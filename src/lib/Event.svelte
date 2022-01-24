<script>
    export let course_summary;
    export let course_description;
    export let course_start;
    export let course_end;
    export let course_location;
    export let course_geo;
    const date_options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
    const time_options = { hour: '2-digit', minute: '2-digit' }

</script>

<article>
    <h3>{course_summary}</h3>
    <h4>{course_start.toLocaleDateString('fr-FR', date_options)}</h4>
    <h5>{course_start.toLocaleTimeString('fr-FR', time_options)} - {course_end.toLocaleTimeString('fr-FR', time_options)} </h5>
    <p>
        {course_description.replaceAll('\\n', '\n').replaceAll('\\', '')}
    </p>
    {#if course_location != undefined}
        <p>
            {course_location.replaceAll('\\n', '\n').replaceAll('\\', '')}
        </p>
    {/if}
    {#if course_geo != undefined}
        {course_geo.replace(';', ', ')}
    {/if}
</article>


<style>
    article {
        background-color: lightgray;
        border-radius: 2px;
        padding: 1px 5px;
    }
    p {
        white-space: pre-wrap;
    }
</style>
