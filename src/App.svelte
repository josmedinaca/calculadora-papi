<script>
  import SubjectForm from "./components/SubjectForm.svelte";
  import SubjectsList from "./components/SubjectsList.svelte";

  let subjects = [];

  function calculatePAPI(subjectsArray) {
    const totalWeightedScores = subjectsArray.reduce(
      (acc, subj) => acc + (subj.cancelled ? 0 : subj.grade * subj.credits), 
      0
    );
    const totalCredits = subjectsArray.reduce(
      (acc, subj) => acc + subj.credits, 
      0
    );
    return totalCredits > 0
      ? (totalWeightedScores / totalCredits).toFixed(2)
      : "0.00";
  }

  function addSubject(subject) {
    subjects = [...subjects, subject];
  }

  function deleteSubject(index) {
    subjects = subjects.filter((_, i) => i !== index);
  }

  $: papi = calculatePAPI(subjects);
</script>

<main>
  <div class="title-container">
    <h1>Calculadora de PAPI</h1>
  </div>
  <SubjectForm on:addSubject={(event) => addSubject(event.detail)} />
  <SubjectsList
    {subjects}
    on:deleteSubject={(event) => deleteSubject(event.detail)}
  />
  <div class="papi-result">PAPI: {papi}</div>
</main>

<style>
  .title {
    text-align: center;
    color: #1976d2;
  }

  .form-group {
    margin-bottom: 20px;
  }

  .label {
    display: block;
    margin-bottom: 5px;
  }

  .btn-group {
    text-align: center;
  }

  .result {
    text-align: center;
    margin-top: 20px;
    font-size: 1.5em;
    font-weight: bold;
  }
</style>
