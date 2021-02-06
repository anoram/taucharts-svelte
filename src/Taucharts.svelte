<script>
    import * as Taucharts from "taucharts";
    import "taucharts/dist/taucharts.min.css";
    import "./plugins";
    export let options;
  
    function action(node, options) {
      let { plugins } = options;
  
      let plg = [];
      if (plugins) {
        plugins.map((e) => {
          plg.push(Taucharts.api.plugins.get(e)());
        });
      }
      options = { ...options, plugins: plg };
      let chart = new Taucharts.Chart(options);
      chart.renderTo(node);
  
      return {
        update(options) {
          chart.updateConfig(options);
        },
        destroy() {
          chart.destroy()
        },
      };
    }
  </script>
  
  <div use:action={options} />
  
  <style>
    div {
      height: inherit;
      width: inherit;
    }
  </style>
  