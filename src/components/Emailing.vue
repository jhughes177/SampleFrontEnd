<template>
<div>
 <div id="emailing">
  <h1>Coding Sample</h1>
  <br>
  <p>Please ensure you have the NodeJS emailing API setup locally</p>
  <br>
  <form id="signup" method="post" v-on:submit.prevent>
  <input v-model="fromEmail" placeholder="From Email" required/><br>
  <input v-model="toEmail" placeholder="To Email" required /><br>
  <input v-model="emailSubject" placeholder="Subject" required/><br>
  <input v-model="emailText" placeholder="Email Text" required/><br>
  <br>
  <button v-on:click="sendEmail" type="submit">Send Email</button>
  </form>
</div>
</div>
</template>
<script>
export default {
  name: 'Emailing',
  methods: {
    sendEmail: function () {
      this.request = {
        from: this.fromEmail,
        to: this.toEmail,
        subject: this.emailSubject,
        text: this.emailText
      };
      console.log(this.request);
  if(this.fromEmail && this.toEmail) { 
    return fetch('http://{replaceWithLocalURI}/sendemail', { //Use local URL for testing NodeJS api ex
      method: 'post',
      mode: 'cors',
      headers: {
        'Accept': 'application/json',
        'Content-type' : 'application/json'
      },
      body: JSON.stringify(this.request)
        }).then(result => {
          console.log(result);
          if(result){
          alert('Email Sent to: ' + this.request.to + '!')
          }
      });
  } else{
    alert('Please provide From and To Email Addresses')
  }    
 
    }
  }
}
</script>
