<template>
  <div class="container">
    <h3 class="form-label">Write Us</h3>
    <form
      name="contact"
      method="post"
      netlify="true"
      netlify-honeypot="bot-field"
    >
      <input type="hidden" name="form-name" value="contact" />
      <div class="contact-info">
        <div class="input-contact-details">
          <input
            id="name"
            v-model="name"
            type="text"
            name="name"
            placeholder="Jayne Tho"
          />
          <label for="name">Name</label>
        </div>
        <div class="input-contact-details">
          <input
            id="email"
            v-model="email"
            type="text"
            name="email"
            placeholder="jayne@tho.com"
            autocomplete="off"
          />
          <label for="email">Email</label>
        </div>
      </div>
      <div class="contact-message">
        Message
        <textarea
          v-model="message"
          placeholder="Hi I'm a placeholder"
        ></textarea>
        <button class="submit-btn">Submit</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: '',
      email: '',
      message: ''
    }
  },
  methods: {
    encode(data) {
      return Object.keys(data)
        .map(
          (key) => `${encodeURIComponent(key)}=${encodeURIComponent(data[key])}`
        )
        .join('&')
    },
    handleSubmit() {
      const data = {
        name: this.name,
        email: this.email,
        message: this.message,
        'form-name': 'contact'
      }
      fetch('/', {
        method: 'POST',
        headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
        body: this.encode(data)
      })
        .then((data) => console.log(data))
        .catch((err) => console.error(err))
    }
  }
}
</script>

<style lang="scss">
$color-text-light: #eaecee;
$color-btn: #cd2d62;

.container {
  background: white;
  position: relative;
  display: flex;
  flex-flow: column;
  height: 500px;
  width: calc(100vw - 700px);
  min-width: 700px;
  border: 1px solid darken(#dcdee0, 30%);
  box-sizing: border-box;
  padding: 50px 30px;
}

form {
  flex-grow: 1;
  display: flex;
  justify-content: space-between;
}

.form-label {
  font-size: 2.5rem;
  margin: 0;
  text-align: left;
  &:after {
    content: '';
    display: block;
    width: 100px;
    height: 5px;
    margin-top: 10px;
    background: $color-btn;
  }
}

input[type='text'] {
  -webkit-appearance: none;
  position: absolute;
  bottom: 0;
  display: block;
  padding-top: 2em;
  border: none;
  margin: 0;
  font-size: 1rem;
  background: white;
  line-height: 1.5rem;
  width: 100%;
  &:active,
  &:focus {
    outline: none;
  }
}

textarea {
  resize: none;
  width: 100%;
  height: 250px;
  margin-top: 20px;
  border: none;
  color: black;
  font-size: 1.25rem;
  box-shadow: inset 0 0 0 5px transparent;
  // background: linear-gradient(
  //    white, white 50%, #333 50%, #333
  // );
  // background-size: 100% 202%;
  border: 5px solid transparent;
  transition: border 0.2s ease;
  &:active,
  &:focus {
    outline: none;
    border: 5px solid #8b9298;
    // background-position: 100% -99%;
    // color: white;
  }
  &:hover {
    cursor: pointer;
    border: 5px solid #8b9298;
  }
}

.contact-info {
  flex: 1;
  padding-top: 2rem;
  font-size: 1.35rem;
  & label {
    display: block;
  }
}

.contact-message {
  font-size: 1.35rem;
  height: 100%;
  flex: 1;
  padding-left: 50px;

  &:before {
    content: '';
    position: absolute;
    left: 50%;
    top: 0;
    display: block;
    width: 5px;
    height: 100%;
    background: $color-text-light;
  }
}

.submit-btn {
  cursor: pointer;
  position: absolute;
  bottom: 0;
  padding: 10px 50px;
  width: calc(50% - 5px);
  right: 0;
  color: white;
  font-size: 1.3rem;
  border: none;
  background: $color-btn;
}

input:focus + label:after,
input:active + label:after,
input:hover + label:after {
  width: 100%;
}

.input-contact-details {
  position: relative;
  color: black;
  height: 80px;
  &:not(:first-child) {
    margin-top: 40px;
  }
}

label {
  position: absolute;
  top: 0;
  margin: 0;
  height: 100%;
  width: 100%;
  &:hover {
    cursor: pointer;
  }
  &:after {
    content: '';
    bottom: 0;
    position: absolute;
    display: block;
    width: 0px;
    height: 5px;
    background: darken(#dcdee0, 30%);
    transition: width 0.3s ease-out;
    z-index: 100;
  }
}
</style>
