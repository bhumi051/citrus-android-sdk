<b> Pro-Guard Changes </b>

   If you are using Proguard in your project add the following lines to your configuration:

<pre>
   -keep class com.squareup.okhttp.** { *; }
   -keep interface com.squareup.okhttp.** { *; }
   -dontwarn com.squareup.okhttp.**
   -dontwarn okio.**
   -dontwarn okio.**
   -dontwarn retrofit.**
   -keep class retrofit.** { *; }
   -keepattributes Signature
   -keepattributes Exceptions
   -keep class com.google.gson.** { *; }
   -keep class com.google.inject.** { *; }
   -keep class org.apache.http.** { *; }
   -keep class org.apache.james.mime4j.** { *; }
   -keep class javax.inject.** { *; }
   -keep class com.citrus.** { *; } 
   -keepattributes *Annotation*
   
   # For facebook crypto library
   # Keep our interfaces so they can be used by other ProGuard rules.
   # See http://sourceforge.net/p/proguard/bugs/466/
   -keep,allowobfuscation @interface com.facebook.crypto.proguard.annotations.DoNotStrip
   -keep,allowobfuscation @interface com.facebook.crypto.proguard.annotations.KeepGettersAndSetters
   
   # Do not strip any method/class that is annotated with @DoNotStrip
   -keep @com.facebook.crypto.proguard.annotations.DoNotStrip class *
   -keepclassmembers class * {
       @com.facebook.crypto.proguard.annotations.DoNotStrip *;
   }
   
   -keepclassmembers @com.facebook.crypto.proguard.annotations.KeepGettersAndSetters class * {
     void set*(***);
     *** get*();
   }
</pre>
