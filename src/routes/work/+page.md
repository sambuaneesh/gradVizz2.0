---
layout: page
title: Behind the Scenes
---

<script>
  import { goto } from '$app/navigation';
</script>

<style>
  .card {
    width: 300px;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    background-color: #fff;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    margin: 20px;
  }

  .card-title {
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 10px;
    color: #333;
  }

  .card-text {
    font-size: 16px;
    color: #666;
    margin-bottom: 20px;
  }

</style>

<div class="flex">
    <div class="card">
        <h2 class="card-title">Brainstorming</h2>
        <p class="card-text">Sneakpeak of how we were trying to brainstorm for ideas.</p>
        <button class="card-button" on:click={() => goto('/work/brain-storming')}>Open</button>
        </div>

        <div class="card">
        <h2 class="card-title">Employability Factor</h2>
        <p class="card-text">Story of how we created a new metric to make our visualizations.</p>
        <button class="card-button" on:click={() => goto('/work/emp-factor')}>Open</button>
    </div>
</div>
