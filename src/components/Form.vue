<template>
    <div id="app">
        <h3>{{title}}</h3>
        <div id="form">
            <input type="text" v-model="name" placeholder="Nome" />
            <input type="number" v-model="phone" placeholder="Telefone" />
            <input type="email" v-model="email" placeholder="E-mail" />
            <button id="add" :disabled="verifyInputs" @click="registerInterested" type="button">Adicionar</button>
        </div>
        <h3>Interessados</h3>
        <table cellspacing="0" cellpadding="0">
            <thead>
                <th>Nome</th>
                <th>Telefone</th>
                <th>E-mail</th>
                <th>Ação</th>
            </thead>
            <tbody>
                <tr v-for="(interested, index) of interestedList" v-bind:key="index" v-bind:class="{ 'grey-line': index % 2 != 0 }">
                    <td>{{ interested.name }}</td>
                    <td>{{ interested.phone }}</td>
                    <td>{{ interested.email }}</td>
                    <td>
                        <button class="table-btn" type="button" @click="removeInterested(index)">Remover</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    data: function() {
        return {
            interestedList: [],
            name: '',
            phone: '',
            email: ''
        }
    },
    props: {
        title: String
    },
    methods: {
        registerInterested: function() {
            const interested = {
                name: this.name,
                phone: this.phone,
                email: this.email
            }
            this.interestedList.push(interested)
            this.name = ''
            this.phone = ''
            this.email = ''
        },
        removeInterested: function(index) {
            this.interestedList.splice(index, 1)
        }
    },
    computed: {
        verifyInputs: function() {
            let verified = false
            if (this.name == '') {
                verified = true
            }
            if (this.phone == '') {
                verified = true
            }
            if (this.email == '') {
                verified = true
            }
            return verified
        }
    }
}
</script>

<style scoped>
* {
    font-family: Arial, Helvetica, sans-serif;
}

#app {
    width: 500px;
}

#form {
    display: flex;
    flex-direction: column;
    width: 250px;
}

input {
    margin-bottom: 10px;
    border-radius: 5px;
    border-style: ridge;
    padding: 7px;
}

#add {
    width: 125px;
    margin-bottom: 10px;
    padding: 7px;
    border-radius: 5px;
    border-style: outset;
    cursor: pointer;
    background-color: rgb(194, 194, 194);
}

.table-btn {
    border-radius: 5px;
    border-style: outset;
    cursor: pointer;
    background-color: rgb(194, 194, 194);
    padding: 4px;
}

table {
    border-style: solid;
    width: 100%;
}

td {
    padding: 10px;
    text-align: center;
}

thead {
    background-color: rgb(194, 194, 194);
}

.grey-line {
    background-color: rgb(223, 223, 223);
}
</style>