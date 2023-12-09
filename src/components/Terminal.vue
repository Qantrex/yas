<!-- Terminal.vue -->

<template>
  <div v-show="terminalVisible" class="terminal">
    <textarea ref="terminalInput" v-model="input" @keydown="handleKeyDown"></textarea>
    <div class="output-area">
      <div>{{ outputText }}</div>
    </div>
  </div>
</template>

<script>
import moment from "moment-timezone";

export default {
  data() {
    return {
      terminalVisible: false,
      input: "",
      outputText: "Output",
      audio: new Audio('src/assets/rick-roll.mp3'),
    };
  },
  methods: {
    output(text) {
      this.outputText = text;
    },
    PlayAudio(options) {
      switch (options) {
        case "play":
          this.audio.play();
          break;
        case "pause":
          this.audio.currentTime = 0;
          this.audio.pause();
          break;
        default:
          this.output("ERROR: Invalid option")
          break;
      }
    },
    toggleTerminal(OnOff) {
      this.terminalVisible = OnOff ?? !this.terminalVisible;
      if (this.terminalVisible && this.$refs.terminalInput) {
        this.$nextTick(() => {
          this.$refs.terminalInput.focus();
        });
      }
    },
    handleGlobalKeyDown(event) {
      if (event.key === ":") {
        event.preventDefault();
        this.toggleTerminal(true);
      }
    },
    handleKeyDown(event) {
      if (event.key === "Enter") {
        event.preventDefault();
        this.executeCommand(this.input.trim());
        this.input = ""; // Clear the input after executing the command
      }
    },
    executeCommand(command) {
      const [mainCommand, ...rest] = command.trim().split(/\s+/);
      const subCommands = [];
      let parameters = [];

      // Extract subcommands and parameters
      for (const part of rest) {
        if (part.startsWith("-")) {
          subCommands.push(part.slice(1)); // Remove the '-' from the subcommand
        } else {
          parameters.push(part);
        }
      }

      switch (mainCommand) {
        case "exit":
        case "q":
          this.toggleTerminal();
          break;
        case "example": // Replace with your actual command
          this.handleExampleCommand(subCommands, parameters);
          break;
        case "calc":
          this.handleCalcCommand(subCommands, parameters);
          break;
        case "time":
          this.handleTimeCommand(subCommands, parameters);
          break;
        case "rl":
          this.handleRLCommand(subCommands, parameters);
          break;
        case "ss":
          this.handleSSCommand(subCommands, parameters);
          break;
        default:
          this.output(`Unknown command: ${mainCommand}`);
      }

      // Update the textarea with the modified output
      this.$nextTick(() => {
        this.$refs.terminalInput.scrollTop = this.$refs.terminalInput.scrollHeight;
      });
    },
    handleRLCommand(subCommands, parameter) {
      if(subCommands[0] === "p" || subCommands[0] === "pause"){
        this.PlayAudio("pause");
        this.output("Stopped music")
      }else if(subCommands[0] === "start" || subCommands[0] === "s"){
        this.PlayAudio("play");
        this.output("Never gonna give you up, never gonna let you down, never gonna run around and desert you")
      }else{
        this.PlayAudio("play");
        this.output("Never gonna give you up, never gonna let you down, never gonna run around and desert you")
      }
    },
    handleCalcCommand(subCommands, parameter) {
      if (subCommands.includes("h")) {
        this.output("-h Brings up this\n-s Brings up the square root of the number");
        return;
      } else if (subCommands.includes("s")) {
        const tocalc = parameter.join(" ");
        try {
          const result = Math.sqrt(tocalc);
          this.output(`--> ${result}`);
        } catch (error) {
          this.output(`Error: ${error}`);
        }
        return;
      }

      const tocalc = parameter.join(" ");
      try {
        const result = eval(tocalc);
        this.output(`--> ${result}`);
      } catch (error) {
        this.output(`Error: ${error}`);
      }
    },
    handleExampleCommand(subCommands, parameter) {
      this.output(`subcommands: ${subCommands} parameter: ${parameter}`);
      console.log("subcommands:", subCommands);
      console.log("Parameter:", parameter);
    },
    handleSSCommand(subCommands, parameter){
      this.output(`Opened Subway Surfers`);
      window.open("https://poki.com/en/g/subway-surfers", "_blank");
    },
    handleTimeCommand(subCommands, parameter) {
      // Default values
      const timezone = 'Europe/Vienna';
      let timeToConvert = moment();

      if (parameter) {
        const parsedTime = moment(parameter, 'YYYY-MM-DDTHH:mm:ss');
        if (parsedTime.isValid()) {
          timeToConvert = parsedTime;
        } else {
          console.error('Invalid time format. Please use YYYY-MM-DDTHH:mm:ss');
          return;
        }
      }

      // Perform timezone conversion
      try {
        const convertedTime = moment.tz(timeToConvert, timezone);
        this.output(`Converted time (${timezone}): ${convertedTime.format('YYYY-MM-DDTHH:mm:ss')}`);
      } catch (error) {
        console.log(`Error during timezone conversion: ${error}`);
      }
    },
  },
  mounted() {
    window.addEventListener("keydown", this.handleGlobalKeyDown);
  },
  beforeDestroy() {
    window.removeEventListener("keydown", this.handleGlobalKeyDown);
  },
};
</script>

<style scoped>
.terminal,
.terminal textarea,
.output-area {
  box-sizing: border-box;
}

.terminal {
  position: fixed;
  width: 100%;
  height: 50%;
  background: rgba(0, 0, 0, 0.8);
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column; /* Stack children vertically */
  z-index: 999;
}

.terminal textarea {
  width: 50%;
  height: 100%;
  background: rgba(0, 0, 0, 0.6);
  color: #fff;
  outline: none;
  font-family: monospace;
  font-size: 32px;
  border: white 2px solid;
  border-radius: 5px;
  resize: none;
  overflow: auto;
  padding: 20px; /* Updated padding */
}

.output-area {
  margin-top: 10px;
  width: 50%;
  background: rgba(0, 0, 0, 0.6);
  color: #fff;
  font-family: monospace;
  font-size: 32px;
  border: white 2px solid;
  border-radius: 5px;
  overflow-y: auto;
  scrollbar-width: none;
  padding: 15px 20px 20px;
}
</style>