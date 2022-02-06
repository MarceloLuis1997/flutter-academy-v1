<template>
  <div>
    <v-row>
      <v-col cols="4">
        <v-card class="mb-2">
          <v-card-title>Introduction to Dart Language</v-card-title>
          <v-card-text>
            Progress:
            {{ progressValue }}
            <v-progress-linear
              color="light-blue"
              height="10"
              :value="progressValue"
              striped
            />
          </v-card-text>
        </v-card>
        <v-card>
          <v-card-title>{{ lesson.title }}</v-card-title>
          <v-card-text>
            {{ lesson.body }}
            <br><br>
            Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.
          </v-card-text>
        </v-card>
      </v-col>
      <v-col cols="8">
        <v-row>
          <iframe
            width="100%"
            height="800px"
            class="mt-3"
            :src="`https://dartpad.dev/embed-flutter.html?sample_id=${lesson.sampleId}&split=60&theme=dark`"
          />
        </v-row>

        <v-row>
          <v-btn
            depressed
            :disabled="lesson.id === 1"
            :to="`/lessons/${lesson.id - 1}`"
          >
            Back
          </v-btn>
          <v-spacer />
          <v-btn
            v-if="lesson.id < lessonsCount"
            depressed
            color="primary"
            :to="`/lessons/${lesson.id + 1}`"
          >
            Next
          </v-btn>
          <v-btn
            v-if="lesson.id === lessonsCount"
            depressed
            color="success"
          >
            Finish Course
          </v-btn>
        </v-row>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import { defineComponent, ref, computed, useRoute, useRouter } from '@nuxtjs/composition-api'

export default defineComponent({
  name: 'Lesson',

  layout: 'lesson',

  setup () {
    const route = useRoute()
    const router = useRouter()

    const id = computed(() => parseInt(route.value.params.id))

    const lessons = ref([
      {
        id: 1,
        sampleId: 'material.FittedBox.1',
        title: 'Lesson 1: FittedBox',
        body: 'In this example, the image is stretched to fill the entire [Container], which would\nnot happen normally without using FittedBox.'
      },
      {
        id: 2,
        sampleId: 'dart.dart_ui.FontFeature.ordinalForms.1',
        title: 'Lesson 2: Ordinal Forms',
        body: 'This is lesson 2'
      },
      {
        id: 3,
        sampleId: 'widgets.AnimatedSize.1',
        title: 'Lesson 3: Animated Size',
        body: 'This is lesson 3'
      },
      {
        id: 4,
        sampleId: 'material.ScaffoldState.showBottomSheet.1',
        title: 'Lesson 4: Bottom Sheet',
        body: 'This is lesson 4'
      }
    ])

    console.log(route)
    console.log(router)

    const lesson = lessons.value.find(l => l.id === id.value)
    const lessonsCount = computed(() => lessons.value.length)

    const progressValue = computed(() => ((id.value - 1) / lessonsCount.value) * 100)

    return {
      lesson,
      lessons,
      lessonsCount,
      progressValue
    }
  }
})
</script>

<style>

</style>
