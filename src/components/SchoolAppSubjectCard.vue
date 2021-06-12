<template>
  <section class="p-4 text-justify rounded-lg shadow-lg bg-gray-50 w-80">
    <div class="h-30">
      <p class="font-bold ">
        Subject:{{ subject.name }}
      </p>
      <p class="mt-2 text-gray-700 line-clamp-4">
        teacher:{{ subject.teacher }}
      </p>
    </div>
    <div>
      Credit:{{ subject.credits }}
    </div>
  </section>
</template>

<script>
export default {
  props: {
    subject: {
      type: Object,
      required: true
    }
  }
}
</script>
