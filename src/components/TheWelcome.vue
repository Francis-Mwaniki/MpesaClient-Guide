<script setup>
import WelcomeItem from "./WelcomeItem.vue";
import DocumentationIcon from "./icons/IconDocumentation.vue";
import ToolingIcon from "./icons/IconTooling.vue";
import EcosystemIcon from "./icons/IconEcosystem.vue";
import CommunityIcon from "./icons/IconCommunity.vue";
import SupportIcon from "./icons/IconSupport.vue";
import { ref } from "vue";

let message = ref([]);
let registerSuccessMsg = ref([]);
let simulateSuccessMsg = ref([]);
let stkSuccessMsg = ref([]);
let stkMsg = ref("");
async function register() {
  console.log("------------register-------------------");
  let url = "http://localhost:5000/register";
  let res = await fetch(url, {
    method: "GET",
    headers: {
      "Content-type": "application/json",
    },
  });
  if (res.ok) {
    let data = await res.json();
    registerSuccessMsg.value = data;
    console.table(data);
    alert("registered successfully");
  } else {
    console.log("error");
  }
}
async function simulate() {
  console.log("------------simulate-------------------");
  let url = "http://localhost:5000/simulate";
  let res = await fetch(url, {
    method: "GET",
    headers: {
      "Content-type": "application/json",
    },
  });
  if (res.ok) {
    let data = await res.json();
    simulateSuccessMsg.value = data;
    console.table(data);

    alert("simulated successfully");
  } else {
    console.log("error");
  }
}
async function stk() {
  console.log("------------push stk-------------------");
  let url = "http://localhost:5000/stk";
  let res = await fetch(url, {
    method: "GET",
    headers: {
      "Content-type": "application/json",
    },
  });
  if (res.ok) {
    let data = await res.json();
    stkSuccessMsg.value = data;
    console.table(data);

    alert("pushed stk  successfully");
    let callbackUrl = "http://localhost:5000/getRes";
    let accessedData = await fetch(callbackUrl, {
      method: "GET",
      headers: {
        "Content-type": "application/json",
      },
    });
    if (accessedData.ok) {
      let data = await accessedData.json();
      stkMsg.value = data;
      console.log(data);
    }
  } else {
    console.log("error");
  }
}

async function stk_push() {
  await register();
  await simulate();
  await stk();
}
</script>

<template>
  <WelcomeItem>
    <template #icon>
      <DocumentationIcon />
    </template>
    <h1 style="font-weight: bolder; text-transform: uppercase">Welcome</h1>
  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <ToolingIcon />
    </template>
    <div>Mpesa Api</div>

    <br />
  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <EcosystemIcon />
    </template>
    <button @click="register" class="btn">Register</button>
  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <CommunityIcon />
    </template>
    <button @click="simulate" class="btn">Simulate</button>
  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <SupportIcon />
    </template>
    <button @click="stk" class="btn">Pay here</button>
  </WelcomeItem>
  <WelcomeItem>
    <template #icon>
      <SupportIcon />
    </template>
    <button @click="stk_push" class="btn">All in one pay</button>
  </WelcomeItem>
  <div class="transaction">{{ message }}</div>
  <WelcomeItem>
    <div class="iconn">Register</div>
    <div class="transaction">{{ registerSuccessMsg }}</div>
  </WelcomeItem>
  <WelcomeItem>
    <div class="iconn">Simulation</div>
    <div class="transaction">{{ simulateSuccessMsg }}</div>
  </WelcomeItem>
  <WelcomeItem>
    <div class="iconn">STK Success</div>
    <div class="transaction">{{ stkSuccessMsg }}</div>
  </WelcomeItem>
  <WelcomeItem>
    <div class="iconn">Success Message</div>
    <div class="transaction">coming soon{{ stkMsg }}</div>
  </WelcomeItem>
</template>
<style>
.btn {
  padding: 20px 30px;
  background-color: teal;
  border: none;
  max-width: 150px;
  border-radius: 20px;
  color: white;
  cursor: pointer;
}
.transaction {
  display: flex;
  margin: auto;
  align-items: center;
  justify-items: center;
}
.iconn {
  padding-right: 5px;
  padding-left: 5px;
  padding-top: 2px;
  padding-bottom: 2px;
  background-color: blue;
  text-align: center;
  border-radius: 2px;
}
</style>
