<script>
export class MotionList extends Array {
  getMotionNames() {
    return this.map((x)=>(x.name));
  }
  reKeyMotions(names) {
    return this.filter((val)=>(names.includes(val.name)));
  }
}
export default {}
</script>
