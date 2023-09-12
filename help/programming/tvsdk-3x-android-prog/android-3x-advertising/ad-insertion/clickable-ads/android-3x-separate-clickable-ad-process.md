---
description: You should separate your player's UI logic from the process that manages ad clicks. One way to do this is to implement multiple fragments for an activity.
title: Separate the clickable ad process
exl-id: d36d3b7f-8fd0-4d8c-a733-c3b79d564fba
---
# Separate the clickable ad process {#separate-the-clickable-ad-process}

You should separate your player's UI logic from the process that manages ad clicks. One way to do this is to implement multiple fragments for an activity.

1. Implement one fragment to contain the `MediaPlayer`.

   This fragment should call `notifyClick()` and will be responsible for video playback. 

   ```java
   public class PlayerFragment extends SherlockFragment { 
       ... 
       public void notifyAdClick () { 
           _mediaPlayer.notifyClick(); 
       } 
       ... 
   } 
   
   ```

1. Implement a different fragment to display a UI element that indicates that an ad is clickable, monitor that UI element, and communicate user clicks to the fragment that contains the `MediaPlayer`.

   This fragment should declare an interface for fragment communication. The fragment captures the interface implementation during its `onAttach()` lifecycle method and can call the interface methods to communicate with the activity.

   ```java
   public class PlayerClickableAdFragment extends SherlockFragment { 
       private ViewGroup viewGroup; 
       private Button button; 
       OnAdUserInteraction callback; 
       @Override 
       public View onCreateView(LayoutInflater inflater,  
                                ViewGroup container,  
                                Bundle savedInstanceState) { 
           // the custom fragment is defined by a custom button 
           viewGroup = (ViewGroup) inflater.inflate(R.layout.fragment_player_clickable_ad,  
                                                    container, false); 
           button = (Button) viewGroup.findViewById(R.id.clickButton); 
    
           // register a click listener to detect user interaction 
           button.setOnClickListener(new View.OnClickListener() { 
               @Override 
               public void onClick(View v) { 
                   // send the event back to the activity 
                   callback.onAdClick(); 
               } 
           }); 
           viewGroup.setVisibility(View.INVISIBLE); 
           return viewGroup; 
       } 
    
       public void hide() { 
           viewGroup.setVisibility(View.INVISIBLE); 
       } 
    
       public void show() { 
           viewGroup.setVisibility(View.VISIBLE);     
       } 
    
       @Override 
       public void onAttach(Activity activity) { 
           super.onAttach(activity); 
           // attaches the interface implementation 
           // if the container activity does not implement the methods  
           // from the interface an exception will be thrown 
           try { 
               callback = (OnAdUserInteraction) activity; 
           } catch (ClassCastException e) { 
               throw new ClassCastException(activity.toString() 
                   + " must implement OnAdUserInteraction"); 
           }     
       } 
    
       // user defined interface that allows fragment communication 
       // must be implemented by the container activity 
       public interface OnAdUserInteraction { 
           public void onAdClick(); 
       } 
   } 
   
   ```
