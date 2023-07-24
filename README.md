import React, { Component } from "react";
import { render } from "react-dom";
import Keyboard from "react-simple-keyboard";
import "react-simple-keyboard/build/css/index.css";
import "./index.css";

class App extends Component {
  state = {
    layoutName: "default",
    input: ""
  };

  onChange = input => {
    this.setState({
      input: input
    });
    console.log("Input changed", input);
  };

  onKeyPress = button => {
    console.log("Button pressed", button);

    /**
     * If you want to handle the shift and caps lock buttons
     */
    if (button === "{shift}" || button === "{lock}") {
      this.handleShift();
    } else if (button === "{alt}") {
      this.handleAlt();
    } else if (button === "{caps}") {
      this.handleCaps();
    } else if (button === "{alpha}") {
      this.handleAlpha();
    } else if (button === "{symbol}") {
      this.handleSymbol();
    }
  };

  handleSymbol = () => {
    let layoutName = this.state.layoutName;
    console.log("symbol ", layoutName);

    this.setState({
      layoutName: layoutName === "symbol" ? "default" : "symbol",
    });
  }

  handleAlpha = () => {
    this.setState({
      layoutName: "default"
    });
  }

  handleCaps = () => {
    let layoutName = this.state.layoutName;
    console.log("caps ", layoutName);

    this.setState({
      layoutName: layoutName === "caps" ? "default" : "caps",
    });
  }


  handleAlt = () => {
    this.setState({
      layoutName: "alt"
    });
  }

  handleShift = () => {
    this.setState({
      layoutName: "shift"
    });
  };

  onChangeInput = event => {
    let input = event.target.value;
    this.setState(
      {
        input: input
      },
      () => {
        this.keyboard.setInput(input);
      }
    );
  };

  render() {
    return (
      <div>
        <input
          value={this.state.input}
          placeholder={"Tap on the virtual keyboard to start"}
          onChange={e => this.onChangeInput(e)}
        />
        <Keyboard
          keyboardRef={r => (this.keyboard = r)}
          onChange={input => this.onChange(input)}
          onKeyPress={button => this.onKeyPress(button)}
          theme={"hg-theme-default hg-layout-default myTheme"}
          layoutName={this.state.layoutName}
          display = {{
            '{bksp}': '⌫',
            '{enter}': 'return',
            '{space}': 'space',
            '{caps}': '⇧',
            '{alt}': '123',
            '{symbol}': '#+=',
            '{alpha}': 'ABC',
          }}
          layout={{
            default: [
              "q w e r t y u i o p",
              "a s d f g h j k l",
              "{caps} z x c v b n m {bksp}",
              "{alt} {space} {enter}"
            ],
            caps: [
              "Q W E R T Y U I O P",
              "A S D F G H J K L",
              "{caps} Z X C V B N M {bksp}",
              "{alt} {space} {enter}"
            ],
            alt: [
              "1 2 3 4 5 6 7 8 9 0",
              '- / : ; ( ) &amp; @ "',
              "{symbol} . , ? ! ' {bksp}",
              "{alpha} {space} {enter}"
            ],
            symbol: [
              "[ ] { } # % ^ * + =",
              '_ \\ | ~ < > $ £ € ·',
              "{alt} . , ? ! ' {bksp}",
              "{alpha} {space} {enter}"
            ]
          }}
        />
      </div>
    );
  }
}

render(<App />, document.getElementById("root"));
