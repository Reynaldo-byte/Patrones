# Adapter
## Definición

El patrón **adapter** funciona como un puente entre dos interfaces incompatibles. Este tipo de patrón de diseño viene bajo un patrón estructural ya que este patrón combina la capacidad de dos interfaces independientes.

**_Este patrón involucra una sola clase que es responsable de unir funcionalidades de interfaces independientes o incompatibles._** Un ejemplo de la vida real podría ser un caso de lector de tarjetas que actúa como adaptador entre la tarjeta de memoria y una computadora portátil. Usted conecta la tarjeta de memoria al lector de tarjetas y el lector de tarjetas a la computadora portátil para que la tarjeta de memoria pueda leerse a través de la computadora portátil.

[![N|Solid](https://www.tutorialspoint.com/design_pattern/images/adapter_pattern_uml_diagram.jpg)]
## Codigo del diagrama en JAVA
### MediaPlayer.java
~~~
    public interface MediaPlayer {
        public void play(String audioType, String fileName);
    }
~~~
### AdvancedMediaPlayer.java
~~~
public interface AdvancedMediaPlayer {	
   public void playVlc(String fileName);
   public void playMp4(String fileName);
}
~~~
### VlcPlayer.java
~~~
public class VlcPlayer implements AdvancedMediaPlayer{
   @Override
   public void playVlc(String fileName) {
      System.out.println("Playing vlc file. Name: "+ fileName);		
   }

   @Override
   public void playMp4(String fileName) {
      //do nothing
   }
}
~~~
### Mp4Player.java
~~~
public class Mp4Player implements AdvancedMediaPlayer{

   @Override
   public void playVlc(String fileName) {
      //do nothing
   }

   @Override
   public void playMp4(String fileName) {
      System.out.println("Playing mp4 file. Name: "+ fileName);		
   }
}
~~~
### MediaAdapter.java
~~~
public class MediaAdapter implements MediaPlayer {

   AdvancedMediaPlayer advancedMusicPlayer;

   public MediaAdapter(String audioType){
   
      if(audioType.equalsIgnoreCase("vlc") ){
         advancedMusicPlayer = new VlcPlayer();			
         
      }else if (audioType.equalsIgnoreCase("mp4")){
         advancedMusicPlayer = new Mp4Player();
      }	
   }

   @Override
   public void play(String audioType, String fileName) {
   
      if(audioType.equalsIgnoreCase("vlc")){
         advancedMusicPlayer.playVlc(fileName);
      }
      else if(audioType.equalsIgnoreCase("mp4")){
         advancedMusicPlayer.playMp4(fileName);
      }
   }
}
~~~
### AudioPlayer.java
~~~ 
public class AudioPlayer implements MediaPlayer {
   MediaAdapter mediaAdapter; 
   public void play(String audioType, String fileName) {		

      //inbuilt support to play mp3 music files
      if(audioType.equalsIgnoreCase("mp3")){
         System.out.println("Playing mp3 file. Name: " + fileName);			
      } 
      
      //mediaAdapter is providing support to play other file formats
      else if(audioType.equalsIgnoreCase("vlc") || audioType.equalsIgnoreCase("mp4")){
         mediaAdapter = new MediaAdapter(audioType);
         mediaAdapter.play(audioType, fileName);
      }
      
      else{
         System.out.println("Invalid media. " + audioType + " format not supported");
      }
   }   
}
~~~
### AdapterPatternDemo.java
~~~
public class AdapterPatternDemo {
   public static void main(String[] args) {
      AudioPlayer audioPlayer = new AudioPlayer();

      audioPlayer.play("mp3", "beyond the horizon.mp3");
      audioPlayer.play("mp4", "alone.mp4");
      audioPlayer.play("vlc", "far far away.vlc");
      audioPlayer.play("avi", "mind me.avi");
   }
}
~~~

Con esto queda concluido el patron **Adapter**.
