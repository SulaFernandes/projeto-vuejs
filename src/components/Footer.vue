<template>
    <div id="footer">
        <p>Sula Fernandes &copy; 2022</p>
    </div>
</template>

<script>
export default {
    name: 'Footer'
}
</script>
<style scoped>
  #footer {
    height: 100px;
    background-color: #222;
    border-top: 4px solid #d225f5;
    color: #FFF;
    display: flex;
    align-items: center;
    justify-content: center;
    bottom: 0;
    width: 100%;
  }
  p {
    font-weight: bold;
  }
</style>