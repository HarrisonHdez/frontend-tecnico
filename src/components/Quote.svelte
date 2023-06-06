<script>
    let quote = '';
    let author = '';

    const fetchRandomQuote = async () => {
        try {
            const response = await fetch('https://api.quotable.io/random');
            const data = await response.json();
            quote = data.content;
            author = data.author;
        } catch (error) {
            console.error(error);
        }
    }

  fetchRandomQuote();
</script>

  <em class="card__paragraph">"{quote}"</em>  <span class="card__span"> - {author}</span>


<style>


.card__paragraph {
    color: var(--text-color);
    font-family: 'Lato', sans-serif;
    font-weight: 400;
    font-style: italic;
}
.card__span {
    color: var(--text-color);
    font-family: 'Open Sans', sans-serif;
    font-weight: 400;
}
</style>
