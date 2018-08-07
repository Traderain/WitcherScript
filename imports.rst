Importing classes
===========================

Importing classes is a very important but very tricky feature in WitcherScript. The problem is that you will have conflicts if you import
a class multiple times so its recommended to use the SharedImports: https://www.nexusmods.com/witcher3/mods/2110? mod to resolve these.

Importing a class and using it in a Script
-------

- Run the game with -dumprtti and it will generate an xml file called rttidump.xml
- Create a ws file and inside that follow the guidance of the xml.
Example:
::
    import class CParticleSystem extends CResource
    {
        import var previewBackgroundColor : Color;
        import var previewShowGrid : Bool;
        import var visibleThroughWalls : Bool;
        import var prewarmingTime : Float;
        import var autoHideDistance : Float;
        import var autoHideRange : Float;
        import var renderingPlane : ERenderingPlane;
    }
::
After that you can use it like so:
::
    exec function w2p()
    {
        var particle : CParticleSystem;
        particle = ( CParticleSystem )LoadResource(  "characters\models\common\special\demon_horse\flies.w2p", true );
        theGame.GetGuiManager().ShowNotification("Loaded: characters\models\common\special\demon_horse\flies.w2p" + "<br>" +
         "renderingPlane: " + particle.renderingPlane + "<br>" +
         "previewBackgroundColor: " + "<br>" +
         "   Red:" + particle.previewBackgroundColor.Red + "<br>" + 
         "   Green:" + particle.previewBackgroundColor.Green + "<br>" + 
         "   Blue:" + particle.previewBackgroundColor.Blue + "<br>" + 
         "   Alpha:" + particle.previewBackgroundColor.Alpha + "<br>" + 
         "previewShowGrid: " + particle.previewShowGrid  + "<br>" +
         "visibleThroughWalls: " + particle.visibleThroughWalls  + "<br>" +
         "prewarmingTime: " + particle.prewarmingTime  + "<br>" +
         "autoHideDistance: " + particle.autoHideDistance  + "<br>" +
         "autoHideRange: " + particle.autoHideRange  + "<br>" +
         "renderingPlane: " + particle.renderingPlane);
    }
::
