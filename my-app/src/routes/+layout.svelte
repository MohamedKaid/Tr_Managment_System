<script>
  import '../app.css';
  import { initializeApp } from 'firebase/app';
  import { getAnalytics, isSupported } from 'firebase/analytics';

  const firebaseConfig = {
    // Your Firebase config
  };

  const app = initializeApp(firebaseConfig);

  let analyticsInstance;

  async function initializeFirebaseAnalytics() {
    if (typeof window !== 'undefined' && (await isSupported())) {
      analyticsInstance = getAnalytics(app);
      console.log('Firebase Analytics initialized on the client.');
    } else {
      console.log('Firebase Analytics not supported in this environment.');
    }
  }

  if (typeof window !== 'undefined') {
    initializeFirebaseAnalytics();
  }

  // You can optionally export 'app' if needed elsewhere on the client
  // if (typeof window !== 'undefined') {
  //   export { app };
  // }
</script>

<slot></slot>

<style>
  /* Move your global styles to src/app.css */
</style>