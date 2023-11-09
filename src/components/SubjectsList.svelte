<script>
    import { createEventDispatcher } from 'svelte';
  
    export let subjects;
    const dispatch = createEventDispatcher();
  
    function deleteSubject(index) {
      dispatch('deleteSubject', index);
    }
  </script>
  
  <table>
    <thead>
      <tr>
        <th>Asignatura</th>
        <th>Créditos</th>
        <th>Calificación</th>
        <th></th>
      </tr>
    </thead>
    <tbody>
        {#each subjects as subject, index}
          <tr>
            <td>{subject.name}</td>
            <td>{subject.credits}</td>
            <td>{subject.cancelled ? 'Cancelada' : subject.grade}</td>
            <td><button on:click={() => deleteSubject(index)}>Eliminar</button></td>
          </tr>
        {/each}
      </tbody>
    
  </table>
