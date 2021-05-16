<script>
  import ContactCard from "./ContactCard.svelte";

  let name = "Max";
  let title = "";
  let image = "";
  let description = "";
  let formState = "empty";
  let createdContacts = [];

  const addContact = () => {
    if (
      name.trim().length === 0 ||
      title.trim().length === 0 ||
      description.trim() === 0 ||
      image.trim().length === 0
    ) {
      formState = "invalid";
      return;
    }

    createdContacts.push({
      //svelte nepozná změnu musíme přepsat pole!
      name,
      title,
      description,
      image,
    });

    createdContacts = [ // svelte pozná změnu bo přepisujeme
      ...createdContacts,
      {
        name,
        title,
        description,
        image,
      },
    ];

    formState = "done";
  };
</script>

<div id="form">
  <div class="form-control">
    <label for="userName">User Name</label>
    <input type="text" bind:value={name} id="userName" />
  </div>
  <div class="form-control">
    <label for="jobTitle">Job Title</label>
    <input type="text" bind:value={title} id="jobTitle" />
  </div>
  <div class="form-control">
    <label for="image">Image URL</label>
    <input type="text" bind:value={image} id="image" />
  </div>
  <div class="form-control">
    <label for="desc">Description</label>
    <textarea rows="3" bind:value={description} id="desc" />
  </div>
</div>

<button on:click={addContact}>Add Contact Card</button>
{#if formState === "invalid"}
  <p>invalid input</p>
{:else}
  <p>enter some data</p>
{/if}

{#each createdContacts as contact}
  <ContactCard
    userName={contact.name}
    jobTitle={contact.title}
    description={contact.description}
    userImage={contact.image}
  />
{/each}

<style>
  #form {
    width: 30rem;
    max-width: 100%;
  }
</style>
