<template>
    <div>
        <h2>Welcome to {{title2}}!</h2>
        <!--value대신 v-model-->
        <input type="text" v-model="input1" />
        <!--onclick대신 @click-->
        <!--@를 사용하여 이벤트를 걸 수 있음-->
        <button type="button" @click="getData">Get</button>
        <button type="button" @click="setData">Set</button>

        <select class="form-control" v-model="region" @change="changeRegion">
            <!--d는 반복하는 코드의 개별 줄 단위...-->
            <option :key="i" :value="d.v" v-for="(d, i) in options">{{d.t}}</option>
        </select>

        <!--v-if: 지정한 조건을 만족하면 해당 element를 rendering (미충족 시 rendering자체가 안됨)-->
        <!--v-show는 무조건 rendering을 함-->
        <table class="table table-bordered" v-if="tableShow">
            <tr :key="i" v-for="(d, i) in options">
                <td>{{d.v}}</td>
                <td>{{d.t}}</td>
            </tr>
        </table>
    </div>
</template>

<script>
export default {
    //script 내 data()에 정의한 데이터들을 사용 및 전송
    //Vue.js는 two-way binding을 제공함
    data() {
        return {
            title: "개발자의 품격",
            title2: "Seoul",
            input1: "abc",
            options: [
                {v:"SSSS",t:"Seoul"},
                {v:"JJJJJ",t:"Jeju"},
                {v:"JGJGJG",t:"JjickGo"}
            ],
            region: "JJJJJ",
            tableShow: true
        };
    },

    //watch: 데이터를 func형태로 만들어 해당 데이터의 변경내용을 추적
    watch: {
        input1() {
            console.log(this.input1);
        }
    },

    //함수 정의는 여기서
    methods: {
        getData() {
            alert(this.input1);
        },
        setData() {
            this.input1 = "I can control this value";
        },
        changeRegion() {
            alert(this.region);
        }
    },

    //Vue.js의 Life Cycle
    /* 
        db를 가져온 후 미리 바인딩해야 할 데이터가 있을 때에는
        mount보다 create에서 작업해 두는 것이 좋다.
        mount과정에 데이터를 바운딩하면 다시 rendering하게 되어 불필요하게 update가 발생하므로
    */
    beforeCreate() {
        console.log("beforeCreate");
    },
    created() {
        console.log("created");
    },
    beforeMount() {
        console.log("beforeMount");
    },
    mounted() {
        console.log("mounted");
    },
    beforeUpdate() {
        console.log("beforeUpdate");
    },
    updated() {
        console.log("updated");
    },
    beforeDestroy() {
        console.log("beforeDestroy");
    },
    destroyed() {
        console.log("destroyed");
    }
}
</script>