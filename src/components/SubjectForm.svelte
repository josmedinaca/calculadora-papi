<script>
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();

    let subjectName = "";
    let credits = "";
    let grade = "";
    let cancelled = false;

    function addSubject() {
        if (subjectName.trim() && credits > 0 && (grade >= 0 || cancelled)) {
            dispatch("addSubject", {
                name: subjectName,
                credits: +credits,
                grade: +grade,
                cancelled: cancelled, 
            });
            subjectName = "";
            credits = "";
            grade = "";
            cancelled = false; 
        }
    }
</script>

<form on:submit|preventDefault={addSubject}>
    <input placeholder="Nombre de la asignatura" bind:value={subjectName} />
    <input type="number" placeholder="Créditos" bind:value={credits} min="0" />
    <input
        type="number"
        placeholder="Nota"
        bind:value={grade}
        min="0"
        max="5"
        step="0.1"
    />
    <div class="checkbox-container">
        <input type="checkbox" id="cancel-checkbox" name="cancel" value="cancelada" class="checkbox-custom" bind:checked={cancelled}/>
        <label for="cancel-checkbox" class="checkbox-label">Asignatura cancelada</label>
    </div>
    
    <button type="submit">Agregar Asignatura</button>
</form>
