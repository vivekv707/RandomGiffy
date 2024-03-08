<script>
    let src = ''
    let alt = ''
    let funny = false
    let cute = false
    let animals = false
    let anime = false
    let fails = false
	const getRandomGif = async () => {
    var tags = '';
    if (funny===true){
      tags += 'funny ';
    }
    if (cute===true){
      tags += 'cute ';
    }
    if (animals===true){
      tags += 'animals ';
    }
    if (anime === true){
      tags += 'anime ';
    }
    if(fails === true){
      tags += 'fails'
    }
		var response = await fetch('https://api.giphy.com/v1/gifs/random?api_key=yoFNfMdEj6vecEtVG8yTClm0XHrMf3kI&tag='+tags+'&rating=pg-13');
		var result = await response.json();

    src = result.data.images.original.url;
    alt = result.data.title
    return result;
	}
	
	let GifPromise = getRandomGif();


</script>
<style>
.main{
    display:flex;
    flex-direction:column;
    align-items:center;
    color:white;
    justify-content:space-evenly;

}
.Gif{
    display:flex;
    flex-direction:column;
}

.watermark{
    width: 300px;
    height:50px;
}

.input-container{
  display:flex;
  flex-direction:row;
  align-items:end;

}
input{
  width: 30px;
  height: 30px;
  margin-left:10px;
  margin-right:10px;
}
label{
  font-size:1.4em;

}

</style>

<div class='main'>
<h1 class='heading'>Random Gif</h1>
<div class='input-container'>
<button on:click={()=>{GifPromise = getRandomGif()}} class='button-6'>
	Generate New GIF
</button>
<div class="checkbox-container">
  <input type="checkbox" id="tag1" name="tag" bind:checked={funny}>
  <label for="tag1">Funny</label>
</div>
<div class="checkbox-container">
  <input type="checkbox" id="tag2" name="tag" bind:checked={cute}>
  <label for="tag2">Cute</label>
</div>
<div class="checkbox-container">
  <input type="checkbox" id="tag3" name="tag" bind:checked={animals}>
  <label for="tag3">Animals</label>
</div>
<div class="checkbox-container">
  <input type="checkbox" id="tag4" name="tag" bind:checked={anime}>
  <label for="tag4">Anime</label>
</div>
<div class="checkbox-container">
  <input type="checkbox" id="tag5" name="tag" bind:checked={fails}>
  <label for="tag5">Fails</label>
</div>
</div>

{#await GifPromise}
	<h2>Loading....</h2>
{:then results}
    <div class='Gif'>
	<img {src} {alt} style="max-height: 500px;width: auto;">
    <h4>Gif Title: {alt} </h4>
    </div>
    <img src='gifywatermark.png' alt='Powered by Giphy' class='watermark' >
    
{:catch err}
	<h2>Error while loading gif :(</h2>
{/await}

</div>
<p style='text-align:right;color:white;position:absolute;bottom:0;right:0;margin-right:1em' > Some tags may not work well together :) </p>