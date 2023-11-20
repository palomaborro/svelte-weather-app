<script>
const url = 'https://weatherapi-com.p.rapidapi.com/current.json?q=Buenos%20Aires';
const options = {
	method: 'GET',
	headers: {
		'X-RapidAPI-Key': 'b442ee4687msh6925c6e6fb58c07p1a717ejsnf241116921ed',
		'X-RapidAPI-Host': 'weatherapi-com.p.rapidapi.com'
	}
};
    
    const weatherPromise = fetch(url, options)
      .then((response) => {
        return response.json()
      })
      .then((data) => {
        const { location, current} = data;
        const { country, localtime, name} = location;
        const {condition, humidity, feelslike_c, temp_c, is_day, wind_kph, wind_dir} = current;
        const { code, text} = condition;

        return {
            code,
            text,
            country,
            localtime,
            name,
            condition,
            humidity,
            feelslike_c,
            temperature: temp_c,
            isDay: is_day,
            windSpeed: wind_kph,
            windDirection: wind_dir,
        }
      })
      .catch(err => {
        console.error(err);
      });
    </script>
    
{#await weatherPromise then weather}
<h1>{weather.text}</h1>
{/await}

<h1>Lo que está renderizando</h1>



<style>
    h1 {
        font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    }
</style>