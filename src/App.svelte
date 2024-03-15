<script>
  import { onMount } from 'svelte';
  import svelteLogo from "./assets/upload-svgrepo-com.svg";

  let email = "";

  function refreshPage() {
    location.reload();
  }

  async function onSubmit(event) {
    event.preventDefault();
    const form = document.getElementById("myForm");
    form.classList.add("fadeOut");
    try {
      const response = await fetch('http://emails1.merkulov.ai/save-text', {
        method: 'POST',
        headers: {
          'Content-Type': 'text/plain',
        },
        body: email,
      });
      if (response.ok) {
        setTimeout(function () {
          form.style.display = "none";
          waitlistMessage();
        }, 500);
      } else {
        console.error('Failed to send email');
      }
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
    // Your existing textHoverEffect function
  }

  onMount(() => {
    document.getElementById("waitlistMessage").style.display = "none";
  });
</script>

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
