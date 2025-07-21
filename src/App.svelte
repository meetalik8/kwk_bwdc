<script>
  import TitleSection from "./sections/TitleSection.svelte";
  import IntroSection from "./sections/IntroSection.svelte"
  import PopulationDemographic from "./sections/PopulationDemographic.svelte";
  import EducationDemographic from "./sections/EducationDemographic.svelte";
  import NationalOccupationSection from "./sections/NationalOccupationSection.svelte";
  import StateOccupationSection from "./sections/StateOccupationSection.svelte";
  import CountyOccupationSection from "./sections/CountyOccupationSection.svelte";
  import FinalSection from "./sections/FinalSection.svelte";
</script>

<main>
  <TitleSection />
  <IntroSection />
  <PopulationDemographic />
  <EducationDemographic />
  <NationalOccupationSection />
  <StateOccupationSection />
  <CountyOccupationSection />
  <FinalSection />
</main>
