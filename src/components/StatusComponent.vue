<template>
    <div>
        <v-layout align-strech justify-center row>
            <template v-for="(users, index) in dataColumns">
                <v-flex md4 :class="'card-wrap'" :key="index">
                    <v-card light :class="'card'" height="100%">
                        <v-card-title :class="['subheading', 'font-weight-medium', 'status-title']">{{ status[index] }}</v-card-title>
                        <v-btn :class="['button-status', 'button-prev']"
                            absolute
                            dark
                            fab
                            color="pink"
                            @click="sendToStatus(index)"
                            >
                            <v-icon >mdi-chevron-right</v-icon>
                        </v-btn>
                        <v-btn :class="['button-status', 'button-next']"
                            absolute
                            dark
                            fab
                            color="pink"
                            @click="sendToStatus(index)"
                            >
                            <v-icon>mdi-chevron-left</v-icon>
                        </v-btn>
                        <v-list>
                            <v-list-tile
                                v-for="user in users"
                                :key="user.id"
                                avatar
                                @click="selectItem($event, user, index)"
                                
                            >
                
                                <v-list-tile-avatar>
                                    <img :src="user.profilePic" :class="[{'list-item-active': user.checked }]">
                                </v-list-tile-avatar>

                                <v-list-tile-content>
                                    <v-list-tile-title v-text="user.username" :class="['list-item-title', 'font-weight-medium']"></v-list-tile-title>
                                </v-list-tile-content>

                            </v-list-tile>
                        </v-list>
                    </v-card>
                </v-flex>
            </template>
        </v-layout>
    </div>
</template>

<script>
    export default {
        props: {
            columns: {
                type: Array,
                default: () => [],
            }
        },
        data: () => {
            return {
                dataColumns: [],
                payload: {
                    index: null,
                    users: []
                },
                lastChecked: null,
                inBetween: false,
                ctrlKeyHasPressed: false
            }
        },
        created() {
            this.dataColumns = this.columns;
            this.status = this.getStatus();
        },
        methods: {
            getStatus() {
                return this.dataColumns.map(column => column.reduce((acc, next) => { 
                    acc = next.status !== acc ? next.status : acc;
                    return acc;
                }, ''))
            },
            getColumnByIndex(index) {
                return this.dataColumns[index];
            },
            setColumnByIndex(index, values = []) {
                this.dataColumns[index] = values;
            },
            sendToStatus(index) {

                if(this.payload.index === index) {
                    return false;
                }
                
                if(this.payload.users.length <= 0) {
                    return false;
                }
                
                let users = this.getColumnByIndex(this.payload.index).filter((user) => {
                    return this.payload.users.indexOf(user) === -1;
                });

                this.payload.users.forEach(user => {
                    user.status = this.status[index];
                    delete user.checked;
                });

                this.setColumnByIndex(this.payload.index, [...users]);
                this.setColumnByIndex(index, [...this.getColumnByIndex(index),...this.payload.users]);
                
                this.payload = {
                    index: null,
                    users: []
                };

                this.ctrlKeyHasPressed = false;                

                this.$forceUpdate();                
                this.$emit('status-change', this.dataColumns);
            },
            addUser(user, { shiftKey, columnIndex }) {
               
                if(this.ctrlKeyHasPressed && this.payload.users.length) {
                    this.resetUsersByColumnIndex(columnIndex);
                    this.ctrlKeyHasPressed = false;
                    return false;
                } else {
                    user.checked = true;
                }

                if (this.lastChecked === user) {
                    this.lastChecked = null;
                }

                if (!this.lastChecked && this.payload.users.length > 1) {
                    this.resetUsersByColumnIndex(columnIndex);
                    return false;
                }

                if (shiftKey && user.checked && this.lastChecked) {
                    
                    this.getColumnByIndex(columnIndex).forEach(userColumn => {
                        if (userColumn === user || userColumn === this.lastChecked) {
                            this.inBetween = !this.inBetween;
                        }

                        if (this.inBetween) {
                            userColumn.checked = true;
                        }
                        
                        if (userColumn.checked && userColumn !== this.lastChecked) {
                            this.payload.users.push(userColumn);
                        }
                    });

                    this.lastChecked = null;

                } else {
                    this.lastChecked = user;
                    this.payload.users = [user];
                }

            },
            addUserByMeta(user) {
                user.checked = true;
                this.payload.users.push(user);
            },
            removeUserByIndex(user, index) {
                user.checked = false;
                this.payload.users.splice(index, 1);                        
            },
            getUserIndexFromPayload(user) {
                return this.payload.users.indexOf(user);
            },
            resetUsersByColumnIndex(index) {
                this.getColumnByIndex(index).forEach(user => user.checked = false);
                this.payload.users = [];
            },
            selectItem($event, user, index) {
                const { shiftKey } = $event;

                const userIndex = this.getUserIndexFromPayload(user);

                if(this.payload.index === null) {
                    this.payload.index = index;
                }

                if(this.payload.index !== index) {
                    this.resetUsersByColumnIndex(this.payload.index);
                    this.addUser(user, { 
                        shiftKey: false, 
                        columnIndex: index 
                    });
                } else {
                    
                    if ($event.ctrlKey || $event.metaKey) {
                        this.ctrlKeyHasPressed = true;

                        if (userIndex >= 0) {
                            this.removeUserByIndex(user, userIndex);
                            this.lastChecked = null;
                        } else {
                            this.addUserByMeta(user);
                        }

                    } else {

                        if(!shiftKey && this.payload.users.length >= 1) {
                            this.resetUsersByColumnIndex(index);
                        }
                        
                        if (userIndex >= 0) {
                            this.removeUserByIndex(user, userIndex);
                            this.lastChecked = null;
                        } else {
                            this.addUser(user, { 
                                shiftKey: $event.shiftKey, 
                                columnIndex: index 
                            });
                        }
                        
                    }
                }
                
                this.payload.index = index;
                this.$forceUpdate();
            }
        }
    }
</script>

<style lang="scss">

    .status-title {
        color: #7a7a7a;
    }

    .card-wrap {

        &:first-of-type {
            .button-prev {
                display: none;
            }
        }

        &:last-of-type {
            .button-next {
                display: none;
            }
        }
    }

    .card {
        padding: 40px 30px;
        margin: 0 2px;
        min-height: 430px;
    }

    .list-item-title {
        color: #333;
    }

    .list-item-active {
        border: 3px solid #00dcff;
        box-sizing: content-box;
    }

    .button-status {
        top: 50%;
    }

    .button-prev {
        left: 0;
        transform: translate(-50%, -50%);
        margin-top: -50px;
        margin-left: -2px;
    }

    .button-next {
        right: 0;
        transform: translate(50%, -50%);
        margin-top: 50px;
        margin-right: -2px;
    }
</style>