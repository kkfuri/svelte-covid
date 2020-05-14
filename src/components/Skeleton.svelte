<script>
  import SkeletonItem from "./SkeletonItem.svelte";
</script>

<style>
  .placeholder {
    display: flex;
    flex-direction: column;
    height: 142px;
    border: 2px solid #ccc;
  }
</style>

<div class="placeholder">
  <div style="margin: 24px auto; display: flex; align-items: center">
    <SkeletonItem height={24} width={100} margin="0 20px 0 0" />
    <SkeletonItem height={30} width={45} />
  </div>
  <SkeletonItem height={18} width={140} margin="0 auto" />
  <SkeletonItem height={18} width={100} margin="4px auto" />
</div>
