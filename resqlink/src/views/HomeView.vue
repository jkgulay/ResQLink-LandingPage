<script setup>
import { ref, onMounted } from 'vue'

// Features data
const features = [
  {
    icon: 'mdi-access-point',
    title: 'Peer-to-Peer Messaging',
    description: 'Send SOS alerts via Wi-Fi Direct when offline or out of signal range.',
  },
  {
    icon: 'mdi-map-marker-radius',
    title: 'Offline Location Sharing',
    description: 'Automatically cache and send your last known location to rescuers.',
  },
  {
    icon: 'mdi-account-group',
    title: 'Nearby Responder Detection',
    description: 'Discover and connect with nearby users during a disaster.',
  },
  {
    icon: 'mdi-battery-70',
    title: 'Low Power Mode',
    description: 'Optimized for use during blackouts and low-battery emergencies.',
  },
]

// Testimonials data
const testimonials = [
  {
    name: 'Sarah Johnson',
    role: 'Hiking Enthusiast',
    content:
      'ResQLink saved my friend when we got lost on a trail. The location sharing feature helped rescue teams find us quickly.',
    avatar: 'https://randomuser.me/api/portraits/women/1.jpg', // Using placeholder to avoid external URLs
  },
  {
    name: 'Michael Chen',
    role: 'Parent',
    content:
      'As a parent, having ResQLink gives me peace of mind knowing my family has access to emergency resources at all times.',
    avatar: 'https://randomuser.me/api/portraits/men/91.jpg',
  },
  {
    name: 'Emma Rodriguez',
    role: 'Emergency Responder',
    content:
      'The information provided through ResQLink has helped us reach people faster and with better preparation.',
    avatar: 'https://randomuser.me/api/portraits/women/91.jpg',
  },
]

// Nav links for better maintainability
const navLinks = [
  { title: 'Home', icon: 'mdi-home', href: '#' },
  { title: 'Features', icon: 'mdi-star', href: '#features' },
  { title: 'How It Works', icon: 'mdi-information-outline', href: '#how-it-works' },
  { title: 'Testimonials', icon: 'mdi-account-group', href: '#testimonials' },
  { title: 'Download', icon: 'mdi-download', href: '#download' },
  { title: 'Contact', icon: 'mdi-email', href: '#contact' },
]

// Reactive states
const drawer = ref(false)
const dialog = ref(false)
const themeColor = ref('blue-grey-darken-3')
const scrolled = ref(false)

// Handle scroll for navbar effects
const handleScroll = () => {
  scrolled.value = window.scrollY > 50
}

// Lifecycle hooks
onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})
</script>

<template>
  <v-app>
    <!-- Navigation Drawer -->
    <v-navigation-drawer v-model="drawer" temporary>
      <v-list>
        <v-list-item
          prepend-avatar="src/assets/1.svg"
          title="ResQLink"
          subtitle="Offline Emergency App"
        ></v-list-item>

        <v-divider></v-divider>

        <v-list-item
          v-for="(item, i) in navLinks"
          :key="i"
          :title="item.title"
          :prepend-icon="item.icon"
          :href="item.href"
          link
          @click="drawer = false"
        ></v-list-item>
      </v-list>
    </v-navigation-drawer>

    <!-- App Bar - with scrolling effect -->
    <v-app-bar
      :color="scrolled ? themeColor : 'transparent'"
      :elevation="scrolled ? 4 : 0"
      prominent
      app
      :class="{ 'app-bar-scrolled': scrolled }"
    >
      <template v-slot:image>
        <v-img
          v-if="scrolled"
          gradient="to top right, rgba(38,50,56,.9), rgba(96,125,139,.8)"
        ></v-img>
      </template>

      <template v-slot:prepend>
        <div class="d-flex align-center">
          <v-img
            src="src/assets/1.svg"
            alt="ResQLink Logo"
            width="48"
            height="48"
            class="ml-2 d-none d-sm-block"
          ></v-img>
          <v-app-bar-nav-icon @click="drawer = !drawer" class="d-sm-none"></v-app-bar-nav-icon>
        </div>
      </template>

      <v-app-bar-title class="text-h4 font-weight-bold font-family-roboto"
        >ResQLink</v-app-bar-title
      >

      <v-spacer></v-spacer>

      <div class="hidden-sm-and-down">
        <v-btn
          v-for="(link, i) in navLinks.slice(1)"
          :key="i"
          variant="text"
          class="mx-1"
          :href="link.href"
        >
          {{ link.title }}
        </v-btn>
      </div>

      <v-btn color="white" variant="elevated" class="ml-4" prepend-icon="mdi-download" rounded>
        Download
      </v-btn>
    </v-app-bar>

    <!-- Main Content -->
    <v-main>
      <!-- Hero Section -->
      <v-container
        fluid
        class="pa-1"
        id="home"
        style="background: linear-gradient(to right, #263238, #455a64); min-height: 500px"
      >
        <v-row class="fill-height d-flex align-center justify-center text-center pt-16">
          <v-col cols="12" md="8">
            <h1 class="text-h2 font-weight-bold mb-4 text-white font-family-roboto">
              ResQLink: Offline Emergency App
            </h1>
            <p class="text-h5 mb-6 text-white">
              Stay connected and safe, even without internet—powered by Wi-Fi Direct and
              geolocation.
            </p>

            <div class="d-flex flex-wrap justify-center pt-16">
              <v-btn
                size="x-large"
                color="blue-grey-darken-4"
                class="mx-2 my-2"
                rounded
                prepend-icon="mdi-alarm-light"
                elevation="4"
              >
                Emergency Chat
              </v-btn>
              <v-btn
                size="x-large"
                color="white"
                variant="outlined"
                class="mx-2 my-2"
                rounded
                prepend-icon="mdi-download"
                href="#download"
              >
                Download Now
              </v-btn>
            </div>
          </v-col>
        </v-row>
      </v-container>

      <!-- Features Section -->
      <v-container id="features" class="py-12">
        <v-row>
          <v-col cols="12" class="text-center mb-8">
            <h2 class="text-h3 font-weight-bold mb-2 font-family-roboto">Key Features</h2>
            <p class="text-subtitle-1">
              Essential tools for emergency preparedness when connectivity is limited
            </p>
          </v-col>
        </v-row>

        <v-row>
          <v-col v-for="(feature, i) in features" :key="i" cols="12" sm="6" md="3">
            <v-hover v-slot="{ isHovering, props }">
              <v-card
                v-bind="props"
                :elevation="isHovering ? 12 : 2"
                :class="{ 'on-hover': isHovering }"
                height="100%"
                class="d-flex flex-column"
              >
                <v-card-item>
                  <div class="d-flex flex-column align-center">
                    <v-avatar :class="`bg-${themeColor} mb-4`" size="64" rounded>
                      <v-icon size="32" color="white">
                        {{ feature.icon }}
                      </v-icon>
                    </v-avatar>
                    <v-card-title class="text-h5 font-weight-bold text-center">{{
                      feature.title
                    }}</v-card-title>
                    <v-card-text class="text-body-1 text-center">
                      {{ feature.description }}
                    </v-card-text>
                  </div>
                </v-card-item>
              </v-card>
            </v-hover>
          </v-col>
        </v-row>
      </v-container>

      <!-- How It Works Section -->
      <v-container fluid class="py-12 bg-grey-lighten-4" id="how-it-works">
        <v-container>
          <v-row>
            <v-col cols="12" class="text-center mb-8">
              <h2 class="text-h3 font-weight-bold mb-2 font-family-roboto">How It Works</h2>
              <p class="text-subtitle-1">Simple steps to ensure your safety during emergencies</p>
            </v-col>
          </v-row>

          <v-row align="center">
            <v-col cols="12" md="6" order="2" order-md="1">
              <v-img
                src="/api/placeholder/600/400"
                height="400"
                class="rounded-lg elevation-3"
                cover
              >
                <div class="video-overlay d-flex justify-center align-center fill-height">
                  <v-btn
                    icon="mdi-play"
                    size="x-large"
                    color="white"
                    variant="text"
                    @click="dialog = true"
                    class="play-button"
                  ></v-btn>
                </div>
              </v-img>
            </v-col>
            <v-col cols="12" md="6" order="1" order-md="2">
              <v-timeline align="start">
                <v-timeline-item v-for="n in 3" :key="n" :dot-color="themeColor" size="small">
                  <template v-slot:opposite></template>
                  <div>
                    <h3 class="text-h5 font-weight-bold mb-2">
                      {{
                        [
                          'Install ResQLink',
                          'Enable Offline Location Access',
                          'Send or Receive Emergency Alerts',
                        ][n - 1]
                      }}
                    </h3>
                    <p class="text-body-1">
                      {{
                        [
                          'Install from your app store and open the app to activate emergency mode.',
                          'Allow GPS caching and local mesh scanning to prepare for offline use.',
                          'Use the SOS button or share location with nearby users—even without signal.',
                        ][n - 1]
                      }}
                    </p>
                  </div>
                </v-timeline-item>
              </v-timeline>
              <v-btn
                :color="themeColor"
                size="large"
                class="mt-4"
                prepend-icon="mdi-play-circle"
                @click="dialog = true"
              >
                Watch Demo
              </v-btn>
            </v-col>
          </v-row>
        </v-container>
      </v-container>

      <!-- Testimonials Section -->
      <v-container id="testimonials" class="py-12">
        <v-row>
          <v-col cols="12" class="text-center mb-8">
            <h2 class="text-h3 font-weight-bold mb-2 font-family-roboto">What People Say</h2>
            <p class="text-subtitle-1">Stories from ResQLink users</p>
          </v-col>
        </v-row>

        <v-row>
          <v-col v-for="(testimonial, i) in testimonials" :key="i" cols="12" md="4">
            <v-hover v-slot="{ isHovering, props }">
              <v-card
                v-bind="props"
                class="h-100 testimonial-card"
                :elevation="isHovering ? 8 : 3"
                :class="{ 'on-hover': isHovering }"
              >
                <v-card-item>
                  <v-card-text class="text-body-1">
                    <v-icon color="grey" start>mdi-format-quote-open</v-icon>
                    {{ testimonial.content }}
                    <v-icon color="grey" end>mdi-format-quote-close</v-icon>
                  </v-card-text>
                </v-card-item>
                <v-divider></v-divider>
                <v-card-item class="pt-2">
                  <template v-slot:prepend>
                    <v-avatar size="40">
                      <v-img :src="testimonial.avatar" alt="User Avatar"></v-img>
                    </v-avatar>
                  </template>
                  <v-card-title>{{ testimonial.name }}</v-card-title>
                  <v-card-subtitle>{{ testimonial.role }}</v-card-subtitle>
                </v-card-item>
              </v-card>
            </v-hover>
          </v-col>
        </v-row>
      </v-container>

      <!-- CTA Section -->
      <v-container fluid :class="`py-12 bg-${themeColor} text-center text-white`" id="download">
        <v-container>
          <v-row justify="center">
            <v-col cols="12" md="8">
              <h2 class="text-h3 font-weight-bold mb-6 font-family-roboto">
                Be Prepared for Any Emergency
              </h2>
              <p class="text-h6 mb-8">
                Download ResQLink today and take an important step toward safety and preparedness
                for you and your loved ones.
              </p>

              <div class="d-flex flex-wrap justify-center">
                <v-btn
                  variant="elevated"
                  color="white"
                  :class="`mx-2 my-2 text-${themeColor}`"
                  size="x-large"
                  prepend-icon="mdi-apple"
                  rounded
                >
                  App Store
                </v-btn>
                <v-btn
                  variant="elevated"
                  color="white"
                  :class="`mx-2 my-2 text-${themeColor}`"
                  size="x-large"
                  prepend-icon="mdi-google-play"
                  rounded
                >
                  Google Play
                </v-btn>
              </div>
            </v-col>
          </v-row>
        </v-container>
      </v-container>

      <!-- Contact Section -->
      <v-container id="contact" class="py-12">
        <v-row>
          <v-col cols="12" class="text-center mb-8">
            <h2 class="text-h3 font-weight-bold mb-2 font-family-roboto">Contact Us</h2>
            <p class="text-subtitle-1">Have questions? We're here to help</p>
          </v-col>
        </v-row>

        <v-row>
          <v-col cols="12" md="6">
            <v-card elevation="3" class="pa-4">
              <v-form @submit.prevent="submitForm">
                <v-text-field
                  label="Name"
                  variant="outlined"
                  prepend-inner-icon="mdi-account"
                  density="comfortable"
                  class="mb-2"
                  required
                ></v-text-field>

                <v-text-field
                  label="Email"
                  variant="outlined"
                  prepend-inner-icon="mdi-email"
                  density="comfortable"
                  class="mb-2"
                  type="email"
                  required
                ></v-text-field>

                <v-text-field
                  label="Subject"
                  variant="outlined"
                  prepend-inner-icon="mdi-text-box"
                  density="comfortable"
                  class="mb-2"
                  required
                ></v-text-field>

                <v-textarea
                  label="Message"
                  variant="outlined"
                  prepend-inner-icon="mdi-message-text"
                  rows="4"
                  class="mb-4"
                  required
                ></v-textarea>

                <v-btn
                  :color="themeColor"
                  size="large"
                  block
                  elevation="2"
                  type="submit"
                  prepend-icon="mdi-send"
                >
                  Send Message
                </v-btn>
              </v-form>
            </v-card>
          </v-col>

          <v-col cols="12" md="6">
            <v-card elevation="3" height="100%">
              <v-card-text>
                <div class="d-flex align-center mb-4">
                  <v-avatar :color="themeColor" class="mr-4">
                    <v-icon color="white">mdi-map-marker</v-icon>
                  </v-avatar>
                  <div>
                    <h3 class="text-h6 font-weight-bold">Our Location</h3>
                    <p>123 Safety Street, Secure City, SC 12345</p>
                  </div>
                </div>

                <div class="d-flex align-center mb-4">
                  <v-avatar :color="themeColor" class="mr-4">
                    <v-icon color="white">mdi-phone</v-icon>
                  </v-avatar>
                  <div>
                    <h3 class="text-h6 font-weight-bold">Phone</h3>
                    <p>+1 (555) 123-4567</p>
                  </div>
                </div>

                <div class="d-flex align-center mb-4">
                  <v-avatar :color="themeColor" class="mr-4">
                    <v-icon color="white">mdi-email</v-icon>
                  </v-avatar>
                  <div>
                    <h3 class="text-h6 font-weight-bold">Email</h3>
                    <p>support@resqlink.com</p>
                  </div>
                </div>

                <v-divider class="my-4"></v-divider>

                <h3 class="text-h6 font-weight-bold mb-4">Follow Us</h3>
                <div class="d-flex">
                  <v-btn
                    variant="text"
                    icon="mdi-facebook"
                    class="mr-2"
                    aria-label="Facebook"
                  ></v-btn>
                  <v-btn
                    variant="text"
                    icon="mdi-twitter"
                    class="mr-2"
                    aria-label="Twitter"
                  ></v-btn>
                  <v-btn
                    variant="text"
                    icon="mdi-instagram"
                    class="mr-2"
                    aria-label="Instagram"
                  ></v-btn>
                  <v-btn variant="text" icon="mdi-linkedin" aria-label="LinkedIn"></v-btn>
                </div>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>

    <!-- Footer -->
    <v-footer class="bg-grey-darken-4 text-center d-flex flex-column">
      <div>
        <v-btn
          v-for="(icon, i) in ['mdi-facebook', 'mdi-twitter', 'mdi-linkedin', 'mdi-instagram']"
          :key="i"
          class="mx-2"
          icon
          variant="text"
          :aria-label="['Facebook', 'Twitter', 'LinkedIn', 'Instagram'][i]"
        >
          <v-icon>{{ icon }}</v-icon>
        </v-btn>
      </div>

      <div class="pt-4 pb-3">
        <v-btn
          v-for="(link, i) in ['Home', 'Features', 'About Us', 'Contact', 'Privacy Policy']"
          :key="i"
          variant="text"
          class="mx-2"
          rounded
          :href="i <= 1 ? `#${link.toLowerCase()}` : '#'"
        >
          {{ link }}
        </v-btn>
      </div>

      <v-divider></v-divider>

      <div class="px-4 py-2 text-center w-100">
        {{ new Date().getFullYear() }} — <strong>ResQLink</strong> | Your Safety is Our Priority
      </div>
    </v-footer>

    <!-- Video Dialog -->
    <v-dialog v-model="dialog" width="auto" :scrim="true">
      <v-card>
        <v-card-title class="text-h5 d-flex align-center">
          ResQLink Demo
          <v-spacer></v-spacer>
          <v-btn icon @click="dialog = false" aria-label="Close dialog">
            <v-icon>mdi-close</v-icon>
          </v-btn>
        </v-card-title>
        <v-card-text class="pa-0">
          <v-img
            src="/api/placeholder/720/480"
            height="480"
            width="720"
            class="bg-grey-darken-2"
            cover
          >
            <div class="d-flex justify-center align-center fill-height">
              <v-btn icon="mdi-play" size="x-large" color="white" variant="text"></v-btn>
            </div>
          </v-img>
        </v-card-text>
      </v-card>
    </v-dialog>
  </v-app>
</template>

<style scoped>
/* Global animations and transitions */
.on-hover {
  transition: all 0.3s ease-in-out;
}

/* Hero section styling */
.hero-section {
  background-image: url('/api/placeholder/1600/900');
  background-size: cover;
  background-position: center;
  position: relative;
  min-height: 100vh;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.hero-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.6); /* Darker overlay for better text visibility */
  z-index: 1;
}

.hero-section > * {
  position: relative;
  z-index: 2; /* Bring content above the overlay */
}

/* App bar transition for scroll effect */
.app-bar-scrolled {
  transition:
    background-color 0.3s ease,
    box-shadow 0.3s ease;
}

/* Video overlay styling */
.video-overlay {
  background: rgba(0, 0, 0, 0.3);
  border-radius: 8px;
}

.play-button {
  transform: scale(1);
  transition: transform 0.3s ease;
}

.play-button:hover {
  transform: scale(1.2);
}

/* Testimonial card specific styling */
.testimonial-card {
  transition: transform 0.3s ease;
}

.testimonial-card.on-hover {
  transform: translateY(-10px);
}

/* Dynamic spacing for mobile and desktop */
@media (max-width: 600px) {
  .hero-section {
    min-height: 80vh;
    padding: 0 16px;
  }
}
</style>

<script>
// This can be used for form submission logic when needed
export default {
  methods: {
    submitForm() {
      // Form submission logic here
      console.log('Form submitted!')
      // You could add form validation and API calls here
    },
  },
}
</script>
