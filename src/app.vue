<template>

    <header>
        <h1>
            Create Camera Path
        </h1>
        
    </header>
    <br>
    <h2 style="text-decoration: underline;">Orbit Radius</h2>
    <br>
    <p>How large of a circle for camera path to orbit around object (0 - 4)</p>
    <br>
    <p>Values between 0.5 - 2 work well, smaller numbers for larger scenes</p>
    <br>
    <input type="text" placeholder="Enter Orbit Radius" v-model="radius" />
    <br><br><br>
    <br>
    <h2 style="text-decoration: underline;">Viewing Angle</h2>
    <br>
    <p>Viewing angle to use when orbiting around center of scene (0, 45)</p>
    <br>
    <input type="text" placeholder="Enter Viewing Angle" v-model="angle" />
    <br><br><br><br>

    <button class="btn" v-on:click="getData()">Get camera path JSON</button>

</template>


<script>

export default {
  name: 'App',
  methods:{
      getData()
      {
          // console.log(this.radius, this.angle)
        r_value = this.radius
        a_value = this.angle

        camera_path = {
          "keyframes": [// every 4th value is homogenous coordinate and should remain unchanged
            {          //[X0,Y0,Z0, 0,  X1,Y1,Z1, 0,  X2,Y2,Z2,  0,  X, Y, Z, 1]
              "matrix": [1,0,0,  0,  0,0,1,  0,  0,-1,0,  0,  0,-1*r_value,0,  1],
              "fov": 50,
              "aspect": 1,
              "properties": "[[\"FOV\",50],[\"NAME\",\"Cam 1\"],[\"TIME\",0]]"
            },
            {
              "matrix": [0,1,0,  0,  0,0,1,  0,  1,0,0,  0,  r_value,0,0,  1],
              "fov": 50,
              "aspect": 1,
              "properties": "[[\"FOV\",50],[\"NAME\",\"Cam 2\"],[\"TIME\",0.334]]"
            },
            {
              "matrix": [-1,0,0,  0,  0,0,1,  0,  0,1,0,  0,  0,r_value,0,  1],
              "fov": 50,
              "aspect": 1,
              "properties": "[[\"FOV\",50],[\"NAME\",\"Cam 3\"],[\"TIME\",0.667]]"
            },
            {
              "matrix": [0,-1,0,  0,  0,0,1,  0,  -1,0,0,  0,  -1*r_value,0,0,  1],
              "fov": 50,
              "aspect": 1,
              "properties": "[[\"FOV\",50],[\"NAME\",\"Cam 4\"],[\"TIME\",1]]"
            }
          ],
          "camera_type": "perspective",
          "render_height": 1080,
          "render_width": 1920,
        }

        //                 [X0,X1,X2, X,
        //                  Y0,Y1,Y2, Y,
        //                  Z0,Z1,Z2, Z
        //                   0, 0, 0, 1]
        // frame 1 = keyframe 1
        "camera_to_world": [1, 0, 0, 0,
                            0, 0,-1,-1,
                            0, 1, 0, 0,

                            0, 0, 0, 1],

        // frame 13 = halfway between keyframe 1 and 2
        "camera_to_world": [0.708, 0, 0.706, 0.686,
                            0.706, 0,-0.708,-0.689,
                            0,     1, 0,        0,

                            0,0,0,1],

        //frame 25 = keyframe 2 start
        "camera_to_world": [0, 0, 1, 1,
                            1, 0, 0, 0,
                            0, 1, 0, 0,

                            0,0,0, 1],


      }
    }

}

</script>


<style>

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family:'Courier New', Courier, monospace ;
}

.container {
  max-width: 500px;
  margin: 30px;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
  float: left;
}

code {
  max-width: 500px;
  float: left;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  margin: 30px;
  border-radius: 5px;
}

.btn {
  display: inline-block;
  background: #004d0a;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

</style>