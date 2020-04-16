<template lang="pug">
  #app
    #container
      h1 Directory Structure
      p The following is a proposal for a production-ready directory structure
      br
      b Legend
      li 
        span.purple--text Purple
        |  - Only visible in Ftrack, does not show up on disk
      li 
        span.blue--text Blue
        |  - Created automatically when something is published
      br
      h3 🖱️ Clicking is Encouraged! 👏
      h2 ✨ Project Level
      p You can click through and browse through this full directory example. Further down the page, each part is broken down one by one with some explaination.
      tree-view(
        path="", 
        title="jobs / project"
      )
      h2 ⚠️ Please Read
      li 
        | Every filename, directory name, and version should be 
        span.red--text Linux Friendly 

      li The need for a working area for working on un-published files like "WIP" or "jail" is still undetermined
      li The intent is to abstract this organization through Ftrack's backend and leave the artist to focus on their tasks.
      li
        | Please direct questions to either Luke or Braden as soon as you have them. Whats may seem trivial may not be.

      h2 🧱 Asset Builds
      tree-view(
        path="0|children", 
        title="jobs / project / assets"
      )
      br
      p The Assets folder is where we keep job-specific assets for development over the lifetime of the project. 
      p They are most commonly used in Shots and Sequences. The intent is to work on good assets here and version as we go. 
      p In Ftrack, what we think of as "assets" are called Asset Builds - which are just a collection of versioned parts that make up the asset. These parts are called Asset Versions.
      h2 📦 Asset Versions
      tree-view(
        path="0|children|0|children", 
        title="jobs / project / assets / b52"
      )
      br
      p Asset Version are components that you check in. Stuff like geometry, textures, completed HDA's, etc. They are just like LEGO®'s
      p The benefit to versioning up the smaller pieces of your Asset Build is that it removes production bottleneck and enabled concurrent work. 
      p Another artist working on scene development can pull in your unfinished Asset Version's geometry at v003 and do 90% of their work instead of waiting for you to finish it at v027. Then they can pull the latest version near the end.
      p On disk, the files that you check in (components) are put under name of your Asset Version. 
      p 
        b Example: 
        |  --> fuselage_geo / v003 / alembic.abc
      h2 🎞️ Sequences
      tree-view(
        path="4|children|0|children", 
        title="jobs / project / sequence / sq0010"
      )
      br
      p Sequences and Shots are very similar. The follow the following format on disk:
      p JOBS / PROJECT / sequence / SQ#### / shot / SH####
      p The number of the Sequence or Shot will come from the Storyboard. We use a minimum padding of 10. We can go up #9999 in FTrack. Should be fine 😜
      p There are a few folders. 'assets', 'comp? and 'shot'
      P 'shot' - is a folder where you can find all the shots for the seqence in one place.
      p 'assets' - may look weird, because we already have a project level assets folder. There are some things, especially for scene work, that need to be done on the fly and are specific to shots in a given sequence. An explosion sim is the most common scenario. 
      p We ran into this problem with the last project where the same effect was in many shots, but we had to copy it over to every shot folder instead of keeping it up a level under the sequence.

      h2 🎬 Shots
      tree-view(
        path="4|children|2|children|2|children|3|children", 
        title="jobs / project / sequence / sq0010 / shot / sh0040"
      )
      br 
      p Our idea for Shots is still in progress. Basically check in the .hip or .mb scene file under the scene folder. Publishing is basically the same as an Asset Build.
      p The different render passes that come out of Deadline get checked in as plates under render. This allows the comp artists to work a little bit ahead of schedule.
      p If we are doing Shot level comp work, or at least knocking out the initial bits of it, the 'aep' 'exr' and 'mp4' files get versioned off under 'comp'. The finished .mp4 video is what we can use in our Dailies in Ftrack Review.
      h2 🎨 Comp
      tree-view(
        path="1|children", 
        title="jobs / project / comp"
      )
      br
      p The comp folder can be organized in whatever way. Static assets like sprites that get used across multiple assets don't need checked in.
      p The main that we wanto establish is a folder for After Effects work that will benefit from versioning. So you can publish several Compositions that can be worked on by more than one team member at once.
      h2 🗓️ Preproduction
      tree-view(
        path="2|children", 
        title="jobs / project / preproduction"
      )
      br
      p Organizing all the stuff we get from Customers by: MM_DD_YYYY
      p Having a place to put a Storyboard, Shot List, and Asset List, (and reference, etc...) that is easy to find. Everybody benenfits from it, so putting in a place that is known will go a long ways.
      h2 🎁 Postproduction
      tree-view(
        path="3|children", 
        all,
        title="jobs / project / postproduction"
      )
      br
      p Same as preproduction, but more focused on archving our work as it was delivered and a place to work on post-mortem tasks as needed.
      h2 Suggestions? Lets all talk about it! 🤗
      
</template>

<script>
import TreeView from "./components/TreeView.vue";

export default {
  components: { TreeView },
  data() {
    return {
      dialog: true
    };
  }
};
</script>

<style>
body {
  font-family: "Poppins", sans-serif;
  font-size: 16px;
}

body #app {
  background: #404e5d;
  display: flex;
  justify-content: center;
}

h1 {
  margin: 20px auto 10px auto;
  border-left: 4px solid dodgerblue;
  padding-left: 20px;
}

h2 {
  margin: 90px auto 20px auto;
  border-bottom: 2px solid dodgerblue;
  padding-left: 0px;
  padding-bottom: 4px;
}

#container {
  margin-top: 40px;
  border-radius: 20px;
  margin-bottom: 40px;
  display: block !important;
  background: white;
  padding: 20px 60px;
  max-width: 800px;
}

@media only screen and (max-width: 800px) {
  #container {
    margin-top: 0px;
    margin-bottom: 0px;
    border-radius: 0px;
  }
}
</style>

