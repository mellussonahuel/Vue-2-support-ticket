<template>
    <main>
        <div class="d-flex flex-column w-50 p-2 m-auto">
            <h1 class="p-2">Customer Support Ticket System</h1>
            <input
                placeholder="Ticket Subject"
                class="mt-2"
                v-model="ticket.subject"
            />
            <input
                placeholder="Ticket Description"
                v-model="ticket.description"
                class="mt-2"
            />
            <Dropdown
                v-model="ticket.status"
                :options="creationStatus"
                class="mt-2"
            />
            <button class="mt-2" @click="createTicket">Create Ticket</button>
        </div>

        <div
            class="d-flex flex-column w-50 p-2 m-auto border-top border-bottom mt-5"
        >
            <Dropdown v-model="filter" :options="statuses" class="mt-2" />
        </div>
        <div
            v-if="!tickets.length"
            class="d-flex flex-column w-50 p-2 m-auto mt-5 text-center"
        >
            <h1>No tickets found</h1>
        </div>
        <div
            v-else
            class="d-flex flex-column w-50 p-2 m-auto border-top border-bottom"
            v-for="(ticket, index) in filteredTickets"
            :key="index"
        >
            <Ticket :ticket="ticket">
                <Dropdown
                    v-model="ticket.status"
                    :options="creationStatus"
                    class="mt-2"
                />
            </Ticket>

            <button @click="toggleComment(index)">Add comment</button>

            <Commnent
                v-if="index === commentTicket"
                v-model="comment"
                v-on:add-comment="saveComment(index)"
            />
        </div>
    </main>
</template>

<script>
import Dropdown from "./Dropdown.vue";
import Ticket from "./Ticket.vue";
import Commnent from "./Comment.vue";
export default {
    components: {
        Dropdown,
        Ticket,
        Commnent,
    },
    data() {
        return {
            ticket: this.getInitialTicketState(),
            tickets: [],
            filter: "",
            statuses: ["Show all", "Open", "In Progress", "Closed"],
            currentTicket: null,
            comment: "",
            newStatus: null,
        };
    },
    mounted() {
        this.tickets.push({
            subject: "Subject ticket 1",
            description: "Description ticket 1",
            status: "Open",
            comments: ["A dumy commnet", "another dummy comment"],
        });
        this.tickets.push({
            subject: "Subject ticket 2",
            description: "Description ticket 2",
            status: "In Progress",
            comments: [],
        });
    },
    computed: {
        filteredTickets() {
            return this.filter === "Show all"
                ? this.tickets
                : this.tickets.filter((ticket) => ticket.status != this.filter);
        },
        creationStatus() {
            return this.statuses.filter((status) => status.value != "-");
        },
        commentTicket() {
            return this.currentTicket;
        },
    },
    methods: {
        getInitialTicketState() {
            return {
                subject: "",
                description: "",
                status: "",
                comments: [],
            };
        },
        createTicket() {
            this.tickets.push({ ...this.ticket });
            this.ticket = this.getInitialTicketState();
        },
        updateStatus(index) {},
        toggleComment(index) {
            if (this.currentTicket === index) {
                this.currentTicket = null;
                return;
            }
            this.currentTicket = index;
        },
        saveComment(index) {
            console.log(index, this.comment);
            let ticket = this.tickets[index];
            ticket.comments.push(this.comment);
            this.comment = "";
            this.tickets[index] = ticket;
        },
    },
};
</script>
