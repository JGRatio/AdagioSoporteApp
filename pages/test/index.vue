<template>
  <div>
    <b-button class="mt-2" variant="danger" @click="cancelar">Barras</b-button>
  </div>
</template>

<script>
export default {
  name: 'TestPage',
  layout: 'navFooter',
  data() {
    return {
      filters: {
        id: '',
        issuedBy: '',
        issuedTo: '',
      },
      items: [
        { id: 1234, issuedBy: 'Operator', issuedTo: 'abcd-efgh' },
        { id: 5678, issuedBy: 'User', issuedTo: 'ijkl-mnop' },
      ],
      elements: {
        id: [1234, 5678],
        issuedBy: ['Operator', 'User'],
      },
    }
  },
  computed: {
    filtered() {
      const filtered = this.items.filter((item) => {
        return Object.keys(this.filters).every((key) =>
          String(item[key]).includes(this.filters[key])
        )
      })
      return filtered.length > 0
        ? filtered
        : [
            {
              id: '',
              issuedBy: '',
              issuedTo: '',
            },
          ]
    },
  },
}
</script>

<style lang="scss" scoped></style>
