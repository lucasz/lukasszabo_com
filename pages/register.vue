<template lang="">
    <div>
        register
    </div>
</template>
<script setup>
// pages/register.vue

const client = useSupabaseAuthClient();

async function register() {
  const { firstName, surname, email, password, passwordRepeat } = credentials;
  if (password !== passwordRepeat) return;
  const { error } = await client.auth.signUp({
    email,
    password,
    options: {
      data: {
        first_name: firstName,
        surname,
        email,
      },
      emailRedirectTo: 'http://localhost:3000/login',
    },
  });
  if (error) {
    alert('Something went wrong !');
    return;
  }
  alert('Open the email we sent you to verify your account!');
}
</script>