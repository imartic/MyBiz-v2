<template>
  <q-layout>
    <!--
      Replace following "div" with
      "<router-view class="layout-view">" component
      if using subRoutes
    -->
    <div class="layout-view">

      <div class="layout-padding">
        <br/>
        <h5 class="page-title">Proposal {{this.$route.query.id}}</h5>
        
        <div class="row wrap small-gutter">
            <div class="width-1of2 sm-width-1of1">

                <div class="card bg-white">
                    <div class="card-title">
                        <span>Company data</span>
                        <i id="companySectionIcon" class="expand-btn" @click="companySection = !companySection">
                            expand_less
                        </i>
                    </div>

                    <q-transition name="slide"> <!-- ?: stops just before closing.. -->
                    <div v-if="companySection" class="card-content card-force-top-padding proposal-inputs" id="companySection">
                        <q-autocomplete v-model="company.name"> <!-- todo: load companies then bind to autocomplete -->
                            <div class="floating-label">
                                <input v-model="company.name" required class="full-width">
                                <label>Name</label>
                            </div>
                            
                        </q-autocomplete>
                            <div class="floating-label">
                                <input v-model="company.address" required class="full-width">
                                <label>Address</label>
                            </div>
                            <div class="floating-label">
                                <input v-model="company.city" required class="full-width">
                                <label>City</label>
                            </div>
                            <div class="floating-label">
                                <input v-model="company.phone" required class="full-width">
                                <label>Phone number</label>
                            </div>
                            <div class="floating-label">
                                <input v-model="company.fax" required class="full-width">
                                <label>Fax number</label>
                            </div>
                            <div class="floating-label">
                                <input v-model="company.email" required class="full-width">
                                <label>E-mail address</label>
                            </div>
                            <div class="floating-label">
                                <input v-model="company.pid" required class="full-width">
                                <label>Personal Identification Nubmer</label>
                            </div>
                            <div class="floating-label">
                                <input v-model="company.iban" required class="full-width">
                                <label>IBAN</label>
                            </div>
                        </div>
                    </q-transition>

                </div>
            </div>
            <div class="width-1of2 sm-width-1of1">
                <div class="card bg-white">
                    <div class="card-title">
                        <span>Client data</span>
                        <i id="clientSectionIcon" class="expand-btn" @click="clientSection = !clientSection">
                            expand_less
                        </i>
                    </div>
                    
                    <q-transition name="slide">
                        <div v-if="clientSection" class="card-content card-force-top-padding proposal-inputs" id="clientSection">
                            <q-autocomplete v-model="client.name"> <!-- todo: load companies then bind to autocomplete -->
                                <div class="floating-label">
                                    <input v-model="client.name" required class="full-width">
                                    <label>Name</label>
                                </div>
                            </q-autocomplete>
                            <div class="floating-label">
                                <input v-model="client.address" required class="full-width">
                                <label>Address</label>
                            </div>
                            <div class="floating-label">
                                <input v-model="company.city" required class="full-width">
                                <label>City</label>
                            </div>
                            <div class="floating-label">
                                <input v-model="company.phone" required class="full-width">
                                <label>Phone number</label>
                            </div>
                            <div class="floating-label">
                                <input v-model="company.email" required class="full-width">
                                <label>E-mail address</label>
                            </div>
                            <div class="floating-label">
                                <input v-model="company.pid" required class="full-width">
                                <label>Personal Identification Number</label>
                            </div>
                        </div>
                    </q-transition>

                </div>
            </div>
        </div>

      </div>
    </div>
  </q-layout>
</template>

<script>
export default {
  data () {
    return {
      companySection: true,
      clientSection: true,
      company: {
        name: '',
        address: '',
        city: '',
        phone: '',
        fax: '',
        email: '',
        pid: '',
        iban: ''
      },
      client: {
        name: '',
        address: '',
        city: '',
        phone: '',
        email: '',
        pid: ''
      }
    }
  },
  methods: {
    expandSection (expand, section) {
        if(!expand){
            document.getElementById(section + 'Icon').innerHTML = 'expand_more'
        }
        else{
            document.getElementById(section + 'Icon').innerHTML = 'expand_less'
        }
    }
  },
  watch: {
    companySection: function () {
        this.expandSection(this.companySection, 'companySection')
    },
    clientSection: function (val) {
        this.expandSection(this.clientSection, 'clientSection')
    }
  }
}
</script>

<style lang="stylus" scoped>
.expand-btn
    float right
    cursor pointer
    font-size 22px
.expand-btn:hover
    font-weight 700
.proposal-inputs .floating-label
    margin-bottom 10px
    margin-top 10px
</style>
