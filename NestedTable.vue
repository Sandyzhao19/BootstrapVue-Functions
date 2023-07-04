<template>
    <div>
        <b-row>
            <b-col cols="12">
                <b-table :items="tableItems" :fields="tableFields" responsive>
                    <template #head(add)="data">
                        <b-link>
                            <b-icon icon="plus-circle" scale="1.5" @click="showModal"></b-icon>
                        </b-link>
                    </template>

                    <template v-slot:cell(add)="row">
                        <b-link>
                            <b-icon v-if="row.detailsShowing" icon="chevron-up" scale="1.5"
                                    @click="row.toggleDetails"></b-icon>

                            <b-icon v-else icon="chevron-down" scale="1.5" @click="row.toggleDetails"></b-icon>
                        </b-link>
                    </template>

                    <template v-slot:cell(actions)="row">
                        <b-link>
                            <b-icon icon="trash" scale="1" @click="deleteRow(row.index)"></b-icon>
                        </b-link>
                    </template>

                    <!-- Nested table -->
                    <template #row-details="row">
                        <b-card>
                            <b-table :items="subTableItems" :fields="subTableFields" responsive>
                            </b-table>
                        </b-card>
                    </template>
                </b-table>

                <b-modal v-model="tableModal" size="lg" @hidden="hideModal" title="Add" scrollable ok-title="Save">
                    <!-- Add your own b-modal -->
                    <TableModal />
                </b-modal>
            </b-col>
        </b-row>
    </div>
</template>

<script>
export default {
    name: "NestedTable",
    components: {
        TableModal,
    },
    data() {
        return {
            tableModal: false,
            _showDetails: true,
            tableItems: [
                { name: 'John', age: 25 },
                { name: 'Alice', age: 30 },
                { name: 'Bob', age: 28 },
                { name: 'Emily', age: 35 },
                { name: 'David', age: 32 }
            ],
            tableFields: [
                { key: 'add', label: '' },
                { key: 'name', label: 'Name' },
                { key: 'age', label: 'Age' },
                { key: 'actions', label: 'Actions'}
            ],
            subTableItems: [
                { occupation: 'Engineer', location: 'New York' },
                { occupation: 'Teacher', location: 'London' },
                { occupation: 'Doctor', location: 'Paris' },
                { occupation: 'Artist', location: 'Tokyo' },
                { occupation: 'Lawyer', location: 'Sydney' }
            ],
            subTableFields: [
                { key: 'occupation', label: 'Occupation' },
                { key: 'location', label: 'Location' }
            ]
        }
    },
    methods: {
        showModal() {
            this.tableModal = true;
        },
        hideModal() {
            this.tableModal = false;
        },
        deleteRow(index) {
            this.tableItems.splice(index, 1);
        }
    }
}
</script>

<style>
{/* Add your style */}
<style>
