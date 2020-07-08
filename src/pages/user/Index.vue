<template>
  <q-page padding>
    <div class="q-mb-xl">
      <q-carousel
      animated
      v-model="slide"
      navigation
      infinite
      autoplay
      arrows
      swipeable
      transition-prev="slide-right"
      transition-next="slide-left"
    >
      <q-carousel-slide :name="1" img-src="https://cdn.quasar.dev/img/mountains.jpg" />
      <q-carousel-slide :name="2" img-src="https://cdn.quasar.dev/img/parallax1.jpg" />
      <q-carousel-slide :name="3" img-src="https://cdn.quasar.dev/img/parallax2.jpg" />
      <q-carousel-slide :name="4" img-src="https://cdn.quasar.dev/img/quasar.jpg" />
    </q-carousel>
    </div>
    <div class="row q-col-gutter-md">
      <div class="col-md-3 col-xs-12" v-form="(movie, i) in data" :key="i">
        <q-card>
          <q-img src="https://th.bing.com/th/id/OIP.iTV6u-9_o6n81A0UspQK2QHaE5?pid=Api&rs=1" />

          <q-card-section>
            <q-btn
              fab
              color="red"
              icon="add_shopping_cart"
              class="absolute"
              unelevated
              style="top: 0; right: 12px; transform: translateY(-50%);"
            />

            <div class="row no-wrap items-center">
              <div class="col text-h6 ellipsis">
                Avenger
              </div>
            </div>

            <q-rating v-model="stars" color="orange-5" :max="5" size="32px" />
          </q-card-section>

          <q-card-section class="q-pt-none">
            <div class="text-subtitle1">
              Action
            </div>
            <div class="text-caption text-grey ellipsis-3-lines">
              Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolore magnam mollitia repellendus? Culpa eum quo eveniet dolorem alias totam amet voluptatibus dicta et. Aliquid incidunt qui ipsam voluptates. Earum, minus.
            </div>
          </q-card-section>

          <q-card-actions>
            <q-btn unelevated @click="dialog = true" class="full-width" color="primary">
              Order Now
            </q-btn>
          </q-card-actions>
        </q-card>
        </div>
        <q-dialog v-model="dialog" position="bottom">
      <q-card style="width: 500px">
        <q-card-section>
          <div class="text-h6">Detail Pemesanan</div>
        </q-card-section>
        <q-card-section style="max-height: 50vh;" class="scroll">
          Avenger - Rp. 50.000
          <q-form class="q-mt-md">
            <q-input filled type="number" label="Masukkan Jjumlah" />
             <q-file color="teal" class="q-mt-md" filled v-model="model" label="Label">
                <template v-slot:prepend>
                  <q-icon name="cloud_upload" />
                </template>
      </q-file>
          </q-form>
        </q-card-section>
        <q-card-actions align="right">
          <q-btn flat label="Batal" v-close-popup/>
          <q-btn color="primary" label="Proses"/>
        </q-card-actions>
      </q-card>
    </q-dialog>
    </div>
  </q-page>
</template>
<script>
export default {
  data () {
    return {
      slide: 1,
      stars: 4,
      dialog: false,
      data: []
    }
  },
  created () {
    this.getData()
  },
  methods: {
    getData () {
      this.$axios.get('movie/getall')
        .then(res => {
          if (res.data.sukses) {
            this.data = res.data
          } else {
            this.$showNotif(res.data.pesan, 'negative')
          }
        })
    }
  }
}
</script>
