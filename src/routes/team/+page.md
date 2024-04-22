---
layout: page
title: " "
description: About the Team
---

<div class="flex justify-center">
    <h1>Meet the Team</h1>
</div>

<script>
  const teamMembers = [
    {
      id: '2023121012',
      name: 'Aneesh Sambu',
      personalLink: 'https://github.com/sambuaneesh',
      photoLink: 'https://avatars.githubusercontent.com/u/75294086?v=4',
    },
    {
      id: '2022111029',
      name: 'Pavitra Pinninti',
      personalLink: 'https://github.com/PavitraPi',
      photoLink: 'https://avatars.githubusercontent.com/u/115882827?v=4',
    },
    {
      id: '2022101119',
      name: 'Paridhi Jain',
      personalLink: 'https://github.com/paridhii16',
      photoLink: 'https://avatars.githubusercontent.com/u/127508683?v=4',
    },
  ];
</script>

<style>
  .team-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 2rem;
    padding: 2rem;
  }

  .team-card {
    width: 200px;
    background-color: #fff;
    border-radius: 12px;
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
    overflow: hidden;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }

  .team-card:hover {
    transform: translateY(-8px);
    box-shadow: 0 16px 24px rgba(0, 0, 0, 0.2);
  }

  .team-photo {
    width: 100%;
    height: 200px;
    object-fit: cover;
  }

  .team-info {
    padding: 1.5rem;
    text-align: center;
    background-color: #f8f8f8;
  }

  .team-name {
    font-size: 1.5rem;
    font-weight: bold;
    margin-bottom: 0.5rem;
    color: #333;
    text-transform: uppercase;
    letter-spacing: 1px;
  }
  
  a {
    text-decoration: none;
  }

  .team-link {
    color: #ff6f61;
    text-decoration: none;
    font-size: 1rem;
    font-weight: 500;
    transition: color 0.3s ease;
  }

  .team-link:hover {
    color: #e64a3a;
  }
</style>

<div class="team-container">
  {#each teamMembers as member}
    <a class="team-card" href={member.personalLink} target="_blank" rel="noopener noreferrer">
      <img class="team-photo" src={member.photoLink} alt={member.name} />
      <div class="team-info">
        <h3 class="team-name">{member.name}</h3>
        <div class="team-link">
          {member.id}
        </div>
      </div>
    </a>
  {/each}
</div>