<script>
  import * as mqtt from 'mqtt'
  import { onMount } from "svelte";

  let client = mqtt.connect("ws://test.mosquitto.org:8081"); 
  let power = 0;

  client.on("connect", () => {
      client.subscribe("power");
    });

  onMount(() => {
    let storedPower = localStorage.getItem("power")
    if (storedPower) {
      power = Number(storedPower)
    }
    client.on("message", (topic, message) => {
      if (topic === "power") {
        let msg = message.toString()
        if (!isNaN(msg)) {
        power = Number(message.toString());
        }
      }
    });
  });
  
function handleChange(event) {
    let newPower = event.target.value;
    if (newPower !== power) {
      client.publish("power", newPower, {retain: true});
      localStorage.setItem("power", newPower)
      power = newPower
    }
  }
  </script>

<power class="flex flex-col justify-items-center items-center mt-40">
    <h1 class="text-3xl font-bold m-5">Мощность:</h1>
    <p class="text-6xl mb-5">{power}%</p>
    <input type="range" bind:value={power} min={0} max={100} on:change={handleChange} />
</power>