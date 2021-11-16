<script>
import Form from './-form.vue'

export default {
  extends: Form,
  async validate({ params }) {
    return await !params.id
  }
}
</script>