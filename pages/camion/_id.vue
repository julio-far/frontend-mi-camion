<script>
import Form from './-form.vue';

export default {
  extends: Form,
  validate ({ params }) {
    return /^\d+$/.test(params.id)
  }
}
</script>