<template>
  <nav text-xl mt-6 inline-flex gap-2 pb-4>
    <RouterLink icon-btn i-carbon-home to="/" />
    <button icon-btn @click="toggleDark()">
      <div dark:i-carbon-moon i-carbon-sun />
    </button>

    <a
      icon-btn i-carbon-logo-github
      rel="noreferrer"
      href="https://github.com/LittleSound/three-exercise"
      target="_blank"
      title="GitHub"
    />
  </nav>
</template>
