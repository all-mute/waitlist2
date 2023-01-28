<script>
  import svelteLogo from "./assets/svelte.svg";

  function refreshPage() {
    location.reload();
  }

  function onSubmit() {
    event.preventDefault();
    const form = document.getElementById("myForm");
    form.classList.add("fadeOut");
    setTimeout(function () {
      form.style.display = "none";
      waitlistMessage();
    }, 500);
  }

  function waitlistMessage() {
    const waitlistMessage = document.getElementById("waitlistMessage");
    waitlistMessage.style.display = "block";
  }

  function textHoverEffect() {
    const letters = "abcdefghijklmnopqrstuvwxyz";
    let iteration = 0;

    let interval = setInterval(() => {
      let element = document.getElementById("waitlistMessage");
      element.innerText = element.innerText
        .split("")
        .map((letter, index) => {
          if (index < iteration) {
            return element.dataset.value[index];
          }
          return letters[Math.floor(Math.random() * 26)];
        })
        .join("");
      if (iteration >= element.dataset.value.length) {
        clearInterval(interval);
      }
      iteration += 1 / 3;
    }, 8);

    document.getElementById("waitlistMessage").onmouseover = (event) => {
      iteration = 0;
    };
  }
</script>

<img
  src={svelteLogo}
  class="logo svelte"
  alt="Svelte Logo"
  on:click={refreshPage}
/>

<h1>Compilator</h1>
<p>
  Reduce your code with 90% using our Svelte compiler. Get exclusive Alpha
  access and several beneficial grants by submitting your email below
</p>
<div class="inputwrapper">
  <form id="myForm">
    <div class="input-button-container">
      <input
        class="form-input"
        type="email"
        id="email"
        name="email"
        placeholder="Enter your email address"
        required
      />
      <input
        class="form-input button"
        type="submit"
        value="Submit"
        on:click={onSubmit}
      />
    </div>
  </form>

  <p
    id="waitlistMessage"
    data-value="You have been added to the waitlist!"
    on:mouseover={textHoverEffect}
  >
    You have been added to the waitlist!
  </p>
</div>

<img
  src="https://www.vinamsolutions.com/wp-content/themes/vinamsolutions/svg/mob_app.svg"
  id="appvector"
  alt=""
/>

<style>
</style>
