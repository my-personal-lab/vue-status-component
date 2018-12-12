<template>
  <v-app>
    <v-content :class="'wrapper'">
        <StatusComponent :columns="getUsers" @status-change="handleChange"/>

        <h1>Saida</h1>

        <pre>{{ dump }}</pre>
    </v-content>
  </v-app>
</template>

<script>
import StatusComponent from './components/StatusComponent'

export default {
    name: 'App',
    components: {
        StatusComponent
    },
    data() {
        return {
            status: [],
        }
    },
    created() {
        this.status = this.getUsers;
    },
    methods: {
        handleChange(data) {
            this.status = [...data];
        }
    },
    computed: {
        dump() {
            return JSON.stringify(this.status, null, 4);
        },
        getUsers() {
            return [
                [
                    {
                        "id": 123,
                        "username": "antunesg",
                        "profilePic": "http://i.pravatar.cc/300?img=1",
                        "first_name": "Antunes",
                        "last_name": "Gerald",
                        "email": "email@teste.com",
                        "unidade": [
                            "Address"
                        ],
                        "status": 'Em pausa',
                        "cpf": "XXXXXXXXXX"
                    },
                    {
                        "id": 34,
                        "username": "robertol",
                        "profilePic": "http://i.pravatar.cc/300?img=2",
                        "first_name": "Roberto",
                        "last_name": "Leal",
                        "email": "email@teste.com",
                        "unidade": [
                            "Address"
                        ],
                        "status": 'Em pausa',
                        "cpf": "XXXXXXXXXX"
                    },
                    {
                        "id": 345,
                        "username": "kabiram",
                        "profilePic": "http://i.pravatar.cc/300?img=3",
                        "first_name": "Kabir",
                        "last_name": "Amber",
                        "email": "email@teste.com",
                        "unidade": [
                            "Address"
                        ],
                        "status": 'Em pausa',
                        "cpf": "XXXXXXXXXX"
                    },
                    {
                        "id": 568,
                        "username": "arthurm",
                        "profilePic": "http://i.pravatar.cc/300?img=4",
                        "first_name": "Arthur",
                        "last_name": "Montanhez",
                        "email": "email@teste.com",
                        "unidade": [
                            "Address"
                        ],
                        "status": 'Em pausa',
                        "cpf": "XXXXXXXXXX"
                    },
                    {
                        "id": 354,
                        "username": "gustateste",
                        "profilePic": "http://i.pravatar.cc/300?img=5",
                        "first_name": "Gustavo",
                        "last_name": "Teste",
                        "email": "email@teste.com",
                        "unidade": [
                            "Address"
                        ],
                        "status": 'Em pausa',
                        "cpf": "XXXXXXXXXX"
                    }
                ],
                [
                    {
                        "id": 1646,
                        "username": "antunesg",
                        "profilePic": "http://i.pravatar.cc/300?img=6",
                        "first_name": "Antunes",
                        "last_name": "Gerald",
                        "email": "email@teste.com",
                        "unidade": [
                            "Address"
                        ],
                        "status": 'Em Progresso',
                        "cpf": "XXXXXXXXXX"
                    },
                    {
                        "id": 676436021,
                        "username": "robertol",
                        "profilePic": "http://i.pravatar.cc/300?img=7",
                        "first_name": "Roberto",
                        "last_name": "Leal",
                        "email": "email@teste.com",
                        "unidade": [
                            "Address"
                        ],
                        "status": 'Em Progresso',
                        "cpf": "XXXXXXXXXX"
                    },
                    {
                        "id": 321354,
                        "username": "kabiram",
                        "profilePic": "http://i.pravatar.cc/300?img=8",
                        "first_name": "Kabir",
                        "last_name": "Amber",
                        "email": "email@teste.com",
                        "unidade": [
                            "Address"
                        ],
                        "status": 'Em Progresso',
                        "cpf": "XXXXXXXXXX"
                    },
                    {
                        "id": 166741,
                        "username": "arthurm",
                        "profilePic": "http://i.pravatar.cc/300?img=9",
                        "first_name": "Arthur",
                        "last_name": "Montanhez",
                        "email": "email@teste.com",
                        "unidade": [
                            "Address"
                        ],
                        "status": 'Em Progresso',
                        "cpf": "XXXXXXXXXX"
                    },
                    {
                        "id": 23514654,
                        "username": "gustateste",
                        "profilePic": "http://i.pravatar.cc/300?img=10",
                        "first_name": "Gustavo",
                        "last_name": "Teste",
                        "email": "email@teste.com",
                        "unidade": [
                            "Address"
                        ],
                        "status": 'Em Progresso',
                        "cpf": "XXXXXXXXXX"
                    }
                ],
                [
                    {
                        "id": 614847,
                        "username": "antunesg",
                        "profilePic": "http://i.pravatar.cc/300?img=11",
                        "first_name": "Antunes",
                        "last_name": "Gerald",
                        "email": "email@teste.com",
                        "unidade": [
                            "Address"
                        ],
                        "status": 'Completo',
                        "cpf": "XXXXXXXXXX"
                    },
                    {
                        "id": 17,
                        "username": "robertol",
                        "profilePic": "http://i.pravatar.cc/300?img=12",
                        "first_name": "Roberto",
                        "last_name": "Leal",
                        "email": "email@teste.com",
                        "unidade": [
                            "Address"
                        ],
                        "status": 'Completo',
                        "cpf": "XXXXXXXXXX"
                    },
                    {
                        "id": 16,
                        "username": "kabiram",
                        "profilePic": "http://i.pravatar.cc/300?img=13",
                        "first_name": "Kabir",
                        "last_name": "Amber",
                        "email": "email@teste.com",
                        "unidade": [
                            "Address"
                        ],
                        "status": 'Completo',
                        "cpf": "XXXXXXXXXX"
                    },
                    {
                        "id": 15,
                        "username": "arthurm",
                        "profilePic": "http://i.pravatar.cc/300?img=14",
                        "first_name": "Arthur",
                        "last_name": "Montanhez",
                        "email": "email@teste.com",
                        "unidade": [
                            "Address"
                        ],
                        "status": 'Completo',
                        "cpf": "XXXXXXXXXX"
                    },
                    {
                        "id": 14,
                        "username": "gustateste",
                        "profilePic": "http://i.pravatar.cc/300?img=15",
                        "first_name": "Gustavo",
                        "last_name": "Teste",
                        "email": "email@teste.com",
                        "unidade": [
                            "Address"
                        ],
                        "status": 'Completo',
                        "cpf": "XXXXXXXXXX"
                    }
                ]
            ]
        }
    }
}
</script>

<style lang="scss">
    .wrapper {
        padding: 40px 20px !important;    
    }
</style>

