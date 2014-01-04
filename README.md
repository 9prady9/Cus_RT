Note: All distances in the property files should follow same metric unit, otherwise undefined results will appear in the
rendering.

scene_properties.xml is used to describe the following properties of the scene. Each tag explains how it pertains to the scene.

	<Scene>
		<targetImage name="filename" outputDirectory="location">
			<resolution width="image width" height="image height"/>
			<antiAlias m="horizontal supersampling" n="vertical supersampling"/>
		</targetImage>
		
		<viewPlane sx="width scale" sy="height scale" eyeToViewPlane="distance"/>
	
		<camera> - position, orientation parameters of camera in 3d space
			<eye x="" y="" z=""/>
			<lookAt  x="" y="" z=""/>
			<up  x="" y="" z=""/>             <!--direction-->
		</camera>
        
        <pointLights count="# of point lights">
                <light sno="kind of identification #">
                        <position  x="" y="" z=""/>
                        <color  red="0 to 1" green="" blue=""/>
                </light>
        </pointLights>
        
        <areaLights count="# of square area lights">
        	<ALight sno="kind of identification #">
        		<center  x="" y="" z=""/>
        		<horizontal  x="" y="" z=""/> <!--direction-->
        		<vertical  x="" y="" z=""/>   <!--direction-->
        		<samples hSamples="horizontal" vSamples="vertical"/>
        		<color  red="0 to 1" green="" blue=""/>
        	</ALight>
        </areaLights>
        
        <specularLight phongExponent="">
        	<color red="0 to 1" green="" blue=""/>
        </specularLight>
        
        <ambientLight intensity="kind of amplification factor">
        	<color red="0 to 1" green="" blue=""/>
        </ambientLight>
        
        <goochGooch>
    		<cool factor="">
	  			<color red="0 to 1" green="" blue=""/>
			</cool>
			<warm factor="">
	  			<color red="0 to 1" green="" blue=""/>
			</warm>
		</goochGooch>
		
		<reflection depth="ray tracing depth" intensity="global factor, convience sake" />
			
		<refraction depth="ray tracing depth" intensity="global factor, convience sake" />
		
		<DOF focalLength="" apertureDiameter="" numOfRays="" />
		
		<ambientOcclusion HitEffectiveDistance="" radialSource="location of radial map" />
		
        <envMap whichOne="[cubeMap|sphereMap]">
        	<cubeMap>
        		<posx></posx>
        		<posx></posx>
        		<posx></posx>
        		<posx></posx>
        		<posx></posx>
        		<posx></posx>
        	</cubeMap>
        	<sphereMap> <!-- made available for future implementation -->
        	</sphereMap>
        </envMap>
        
                    <cubeMap> - textures representing all six sides of cube are provided as posx,negx,posy,negy,posz,negz
                    





objects.xml is used to describe the various objects in the scene.


        <objects> - list of objects in the scene, described using object tag. 
                    There can be 4 types of objects: Plane | Sphere  Quadric | Mesh.
                    Every <object> has common attributes like 'MaterialType', 'TextureType' and 'neta'.
                    MaterialType = diffusive | emissive | refractive | reflective
                    TextureType = SOLID | IMAGE | PROCEDURE
                        SOLID - [made available for future implementation]
                        IMAGE - traditional image texturing.
                        PROCEDURE - currently, default JuliaSet is available. More are to come in future.
                        
                    <motion> - speed attribute and direction of the movement.
                    
                    <texFile> - location of texture file if TextureType is IMAGE
                    
                    <color> - default color of the surface of the object
                    
                    <objFile> - this tag is specified if object type="Mesh" to provide location of the OBJ file.    
                    
                    <haxis>,<vaxis> - can be used to produce shear in 2d for object types=Plane|Sphere|Quadric
                    
                    <scale> - can be used to scale object size
                    
                    
        <object type="Plane" ... >
        
                    <normal> - normal of the plane
                    
                    <point> - point on a plane
        
                    
        <object type="Sphere" ... >
        
                    <center> - center of the sphere
                    
                    <radius> - radius of the sphere
        
                    
        <object type="Quadric" ... >
                    
                    <point> - location of the quadric in world coordinates

                        Quadric general equation is F(x) = A*x^2 + B*x + C = 0
                        Normal to Quadric is its gradient = DELTA(F(x)) / |DELTA(F(x))|
                        Below are unit quadrics centered at origin with main axes in x and y dimensions
                        x^2 + y^2 + z^2 - 1 = 0     is Ellipsoid
                        x^2 + y^2 - 1 = 0, Z=[0,K]  is Cylinder
                        x^2 + y^2 - z^2 = 0         is Cone
                        x^2 + y^2 - z^2 - 1 = 0     is Hyperboloid
                        x^2 + y^2 - z^2 + 1 = 0     is Hyperboloid(mirror to above one)
                        x^2 + y^2 - z = 0           is Paraboloid
                        Swapping dimensions will give variations of these basic shapes.
                        Replacing x,y,z with (x-xc),(y-yc),(z-zc) respectively, will translate the object in world.
                        All such equations can be represented using a single equation given below.
                        SUM(ai2,i goes from 0 to 2) * xi^2 + SUM(ai1, i goes from 0 to 1) * xi + a00 = 0
                        where xi = x0 | x1 | x2 each representing the dimensions of 3D space.
                        Please see below for an example of how values of a02,a12,a22, a01, a11, a21, a00 
                        dictates the shape of the quadrics given above.
                        ----------------------------------------------------------
                        Shape        a02    a12    a22    a01    a11    a21    a00
                        ----------------------------------------------------------
                        Plane        0      0      0      0      0      1      0
                        Ellipsoid    1      1      1      0      0      0      -1
                        Cylinder     1      1      0      0      0      0      -1
                        Cone         1      1      -1     0      0      0      0
                        Hyperboloid  1      1      -1     0      0      0      -1
                        Hyperboloid  1      1      -1     0      0      0      +1
                        Paraboloid   1      1      0      0      0      1      0
                        ----------------------------------------------------------
                        
                    <aValues> - a02,a12,a22, a01, a11, a21, a00
                
