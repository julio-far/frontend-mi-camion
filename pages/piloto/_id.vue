<script>
import Form from './-form.vue';

export default class IdPilotoPage extends Form {
  validate ({ params }) {
    return /^\d+$/.test(params.id)
  }
}
</script>