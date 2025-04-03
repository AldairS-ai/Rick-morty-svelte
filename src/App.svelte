<script>
  import Cards from './lib/cards.svelte'; 
  let caracteres = []; 
  let pagina = 1; 

  async function loadCharacters(){ 
    try {
        const response = await fetch('https://rickandmortyapi.com/api/character?page=' + pagina); 
        if (!response.ok) {
            throw new Error('Network response was not ok');
        }
        const data = await response.json();
        console.log(data);  // Moved inside the try block
        caracteres = data.results; 
    } catch (error) {
        console.error('Error fetching characters:', error);
    } 
  } 

  loadCharacters(); 

  function siguiente(){ 
    pagina++;
    loadCharacters(); // Corrected here
  } 
   
  function anterior(){ 
    pagina--;
    loadCharacters(); // Corrected here
  }
</script>

<h1 class="title">Rick and Morty Svelte</h1> 
<h2 class="title">Pagina: {pagina}</h2> 

<div class="contenedor"> 
  <div class="botones"> 
    <button class="boton" onclick={anterior} disabled={pagina === 1}>Anterior</button> 
    <button class="boton" onclick={siguiente}>Siguiente</button> 
  </div> 
  <div class="grid"> 
    {#each caracteres as caracter} 
      <Cards {caracter}/> 
    {/each} 
  </div> 
</div>
