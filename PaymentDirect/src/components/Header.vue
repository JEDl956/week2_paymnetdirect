<template>
  <header class="top">
    <h1>Payment Direct</h1>
    <p>Split expenses and see who owes what .</p>
  </header>
</template>

<style scoped>
* {
  box-sizing: border-box;
}

:global(body) {
  margin: 0;
  min-height: 100vh;
  display: grid;
  place-items: center;
  padding: 24px;
  font-family: system-ui, sans-serif;
  background: #121212;
  color: #e5e5e5;
}

.top {
  text-align: center;
  margin-bottom: 16px;
}

.top h1 {
  margin: 0;
  color: #ffffff;
}

.top p {
  margin: 4px 0 0;
  color: #b3b3b3;
}

.card {
  width: min(600px, 100%);
  background: #1e1e1e;
  padding: 18px;
  border-radius: 16px;
  box-shadow: 0 10px 24px rgba(0, 0, 0, 0.6);
}

.rowForm {
  display: flex;
  gap: 10px;
  margin-bottom: 12px;
}

input,
select {
  flex: 1;
  padding: 10px;
  border-radius: 10px;
  border: 1px solid #3a3a3a;
  background: #2a2a2a;
  color: #ffffff;
}

input::placeholder {
  color: #9ca3af;
}

button {
  padding: 10px 14px;
  border-radius: 10px;
  border: none;
  background: #3f3f46;
  color: #ffffff;
  cursor: pointer;
}

button:hover {
  background: #52525b;
}

section {
  margin-top: 16px;
}

section h3 {
  margin: 0 0 6px;
  font-size: 14px;
  color: #d4d4d8;
}

.list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: grid;
  gap: 8px;
}

.list li {
  padding: 10px;
  border-radius: 10px;
  background: #262626;
  color: #e5e5e5;
}

.summary li {
  background: #1f2937;
  color: #f9fafb;
}
</style>
