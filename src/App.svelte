<script>
  import { onMount } from 'svelte';
  import axios from 'axios'; // Импортируем axios
  import svelteLogo from "./assets/upload-svgrepo-com.svg";

  let email = "";

  function refreshPage() {
    location.reload();
  }

  async function onSubmit(event) {
    event.preventDefault();
    const form = document.getElementById("myForm");
    form.classList.add("fadeOut");
    const bbbb = JSON.stringify({ "text": email });
    console.log(bbbb);
    try {
      // Используем axios для отправки POST запроса
      const response = await axios({
        method: 'post',
        url: 'https://emails1.merkulov.ai/save-text',
        data: bbbb,
        headers: {
          'Content-Type': 'application/json',
        },
      });
      // Проверяем статус ответа, axios автоматически обрабатывает статусы 200-299 как успешные
      setTimeout(function () {
        form.style.display = "none";
        waitlistMessage();
      }, 500);
    } catch (error) {
      console.error('Error:', error);
    }
  }

  function waitlistMessage() {
    const waitlistMessage = document.getElementById("waitlistMessage");
    waitlistMessage.style.display = "block";
    textHoverEffect();
  }

  function textHoverEffect() {
    // Ваша существующая функция textHoverEffect
  }

  onMount(() => {
    document.getElementById("waitlistMessage").style.display = "none";
  });
</script>

<!-- Ваш HTML и стили остаются без изменений -->


<img src={svelteLogo} class="logo svelte" alt="Svelte Logo" on:click={refreshPage} />

<h1>Compilator</h1>
<p>Reduce your code with 90% using our Svelte compiler. Get exclusive Alpha access and several beneficial grants by submitting your email below.</p>
<div class="inputwrapper">
  <form id="myForm" on:submit={onSubmit}>
    <div class="input-button-container">
      <input class="form-input" type="email" bind:value={email} placeholder="Enter your email address" required />
      <button class="form-input button" type="submit">Submit</button>
    </div>
  </form>

  <p id="waitlistMessage" data-value="You have been added to the waitlist!">You have been added to the waitlist!</p>
</div>

<img src="https://www.vinamsolutions.com/wp-content/themes/vinamsolutions/svg/mob_app.svg" id="appvector" alt="" />

<style>
  /* Add your styles here */
</style>
