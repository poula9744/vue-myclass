<template>
    <div>
        <table>
            <thead>
                <tr>
                    <th>번호</th>
                    <th>이름</th>
                    <th>핸드폰</th>
                    <th>회사</th>
                    <th>성별</th>
                </tr>
            </thead>
            <tbody>
                <tr v-bind:key="i" v-for="(personVo, i) in personList">
                    <td id="no">{{ personVo.no }}</td>
                    <td id="name">{{ personVo.name }}</td>
                    <td id="hp">{{ personVo.hp }}</td>
                    <td id="company">{{ personVo.company }}</td>
                    <td id="gender">{{ personVo.gender }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>


<script>
import axios from 'axios';
export default {
    name: "ListView",
    components: {},
    data() {
        return {
            personList: [],
            personVo: {
                no: "",
                name: "",
                hp: "",
                company: "",
                gender: ""
            }
        };
    },
    methods: {
        getList(){
            console.log("리스트 불러오기");
            axios({
                method: 'get', // put, post, delete
                url: ' https://raw.githubusercontent.com/clz2024-red/api/main/person.json',
                headers: { "Content-Type": "application/json; charset=utf-8" }, //전송타입
                //params: boardVo, //get방식 파라미터로 값이 전달
                //data: boardVo, //put, post, delete 방식 자동으로 JSON으로 변환 전달
                responseType: 'json' //수신타입
            }).then(response => {
                console.log(response.data); //수신데이타
                this.personList = response.data;
            }).catch(error => {
                console.log(error);
            });
        }
    },
    created(){
        this.getList();
    }
};
</script>


<style>
table{
    width: 466px;
    border: 1px solid #000000;
    border-collapse: collapse;
    text-align: center;
}
td{
    border: 1px solid #000000;
}
th{
    border: 1px solid #000000;
    background-color: #d6d6d6;
}
#no{
    width: 40px;
}
#name{
    width: 70px;
}
#hp{
    width: 150px;
}
#comapny{
    width: 160px;
}
#gender{
    width: 40px;
}
</style>
