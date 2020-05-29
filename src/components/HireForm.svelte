<script>
  let hire = "Yes";
  let options = ["Yes", "No"];
  const contactHandler = e => {
    hire = e.target.value;
  };
  // $: console.log($hire);
</script>

<div class="form-container" on:change="{contactHandler}">
  <form action="">

    {#each options as value}
      <label for="">
        <input type="radio" {value} bind:group="{hire}" />
        {value}
        <span class="mark"></span>
      </label>
    {/each}

    <a href="mailto:yujee3153@gmail.com" class="btn">
      {hire === 'Yes' ? 'Click to say hello to me' : 'Let me know your comments'}
    </a>
  </form>
</div>

<style>
  .form-container {
    top: 3%;
    left: 57%;
  }
  a {
    position: absolute;
    text-decoration: none;
    text-align: center;
    width: 7rem;
  }
  div {
    position: absolute;
  }
  form {
    position: relative;
    display: flex;
  }
  input {
    visibility: hidden;
    width: 25px;
    height: 25px;
    padding: 0;
    margin: 0;
    cursor: pointer;
  }
  input:after {
    position: absolute;
    visibility: visible;
    content: "";
    width: 20px;
    height: 20px;
    border: #3a3ca1 solid 1.5px;
  }

  label input:checked ~ .mark:after {
    visibility: visible;
  }

  label {
    position: relative;
    margin: 0 0.2rem;
    cursor: pointer;
    user-select: none;
  }
  .mark {
    position: absolute;
    top: -31%;
    left: 10%;
    font-size: 44px;
  }
  .mark:after {
    content: "/";
    position: absolute;
    visibility: hidden;
    color: #797a89;
  }
  .btn {
    top: 95%;
    left: 0;
    transition: background 0.5s linear;
    border: #3a3ca1 solid 2px;
    padding: 0.2rem;
    font-size: 24px;
    cursor: pointer;
    color: #3a3ca1;
  }

  @media (min-width: 640px) {
    .btn:hover {
      background: rgba(255, 255, 255, 0.742);
    }
  }
</style>
