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
        id: Math.random(), //"unikátní" id musí být číslo nebo string
        name,
        title,
        description,
        image,
      },
    ];

    formState = "done";
  };

  const deleteFirst = () => {
    createdContacts = createdContacts.slice(1);
  }

  const deleteLast = () => {
    createdContacts = createdContacts.slice(0, -1);
  }
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
<button on:click={deleteFirst}>Delete first</button>
<button on:click={deleteLast}>Delete last</button>

{#if formState === "invalid"}
  <p>invalid input</p>
{:else}
  <p>enter some data</p>
{/if}

{#each createdContacts as contact, index (contact.id)} <!--přidá ID pro ContactCard a předejde chybě při mazání. ID zrychlí výkon Svelte protože Svelte nemusí překreslit DOM-->
<h2># {index + 1}</h2>
  <ContactCard
    userName={contact.name}
    jobTitle={contact.title}
    description={contact.description}
    userImage={contact.image}
  />
{:else} <!-- co se stane když je pole prázdné-->
  <p>Please start adding some contacts, non were found!</p>
{/each}

<style>
  #form {
    width: 30rem;
    max-width: 100%;
  }
</style>
