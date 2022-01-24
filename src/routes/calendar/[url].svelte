<!-- src/routes/calendar/[url].svelte -->
<svelte:head>
    <title>EDT: Unistra Sanitizer</title>
</svelte:head>

<script context="module">
    import ICalParser from 'ical-js-parser';
    import Event from '$lib/Event.svelte';

    function convert_value(e) {
        return parseInt(e['dtstart']['value'].substring(0, 8) + e['dtstart']['value'].substring(9, 13))
    }

    export async function load({ params, fetch }) {
        const calendar_link = `https://monemploidutemps.unistra.fr/api/calendar/${params.url}/export`
        const res = await fetch(calendar_link)
        if (res.ok) {
            const data = await res.text() 
            const json_data_elements = ICalParser.toJSON(data)['events'];
            json_data_elements.sort((a, b) => (convert_value(a) < convert_value(b)) ? - 1 : ((convert_value(a) > convert_value(b)) ? 1 : 0))

            return {
                props: {
                    events: json_data_elements
                }
            }
        }
    }
</script>

<script>
    export let events;

    function pprint_json(json_obj) {
        console.log(json_obj['description'])
        console.log(parse_dt_value(json_obj['dtstart']['value']))
        console.log(parse_dt_value(json_obj['dtend']['value']))
        console.log("loc: " + json_obj['location'])
        console.log("geo: " + json_obj['geo'])
        console.log(json_obj['summary'])
        console.log(json_obj['uid'])
    }
    function parse_dt_value(value) {
        // from '2022 02 03 T09 30 00 Z' to '2019-01-01T00:00:00.000Z'  
        return new Date(`${value.substring(0, 4)}-${value.substring(4, 6)}-${value.substring(6, 11)}:${value.substring(11, 13)}:${value.substring(13, 15)}Z`)
    }
</script>



<h1>Mon emploi du temps</h1>

{#each events as e}
    <br>
    <Event 
        course_summary={e['summary']}
        course_description={e['description']}
        course_start={parse_dt_value(e['dtstart']['value'])}
        course_end={parse_dt_value(e['dtend']['value'])}
        course_location={e['location']}
        course_geo={e['geo']}
    />
    {/each}