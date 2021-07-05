import React, {Component} from 'react';
import { StyleSheet, View, Text, TextInput, TouchableOpacity } from 'react-native';
import {Header} from 'react-native-elements';
export default class App extends Component {
   constructor(){
     super();
      this.state = {
        text: '',
        isSearchPressed: false,
        isLoading: false,
        word: "Loading...",
        lexicalCategory: '',
        definition: ""

      };
   }

     getWord=(text)=> {
      var text = text.toLowerCase()
      try {
        var word = dictionary[text]["word"]
        var lexicalCategory = dictionary[text]["lexicalCategory"]
        var definition = dictionary[text]["definition"]
        this.setState({
          "word": word,
          "lexicalCategory": lexicalCategory,
          "definition": definition
        })

      }
      catch(err){
        alert("Sorry this word is not in our database")
        this.setState({
          "text": '',
          "isSearchPressed": false
        })
      }
     }
     
   
render(){
  return(
      <View Style={{flex:1, boderWidth:2}}>
        <Header
           backgroundColor={'purple'}
           centerComponent={{
             text: 'Pocket Dictionary',
             style: {color: '#efff',fontSize: 20},
           }}
        />
        <View style={StyleSheet.inputBoxContainer}>

           <TextInput
             style={StyleSheet.InputButton}
             onChangeText={text => {
                this.setState({
                  text: text,
                  isSearchPressed: false,
                  word: "Loading...",
                  lexicalCategory: "",
                  examples: [],
                  definition: ""
                });
             }}
             value={this.state.text}
          />

          <TouchableOpacity
            styles={styles.searchButton}
            onPress={() => {
              this.setState({isSearchPressed: true});
              this.getWord(this.state.text)
            }}>
            <Text styles={styles.searchText}>Search</Text>
        </TouchableOpacity>
      </View>
      <View Style={styles.outputContainer}>
        <Text style={{fontSize: 20}}>
          {
             this.state.isButtonPressed && this.state.word=== "Loading..."
             ? this.state.word
             : ""
          }
        </Text>
          {
             this.state.word !== "Loading..." ?
             (
               <View style={{justifyContent: 'center', marginLeft:10 }}>
                 <View style={styles.detailsContainer}>
                   <Text style={styles.detailsTitle}>
                      Word: {" "}
                    </Text>
                  </View>
                  <View style={styles.detailsContainer}>
                   <Text style={styles.detailsTitle}>
                      Type: {" "}
                    </Text>
                    <Text  style={{fontSize:18}}> 
                      {this.state.lexicalCategory}
                  </Text>
                </View>
                <View style={{flexDirection: 'row', flexWrap: 'wrap'}}>
                <Text style={styles.detailsTitle}> 
                Definition: {" "}
              </Text>
              <Text style={{fontSize:18}}>
                {this.state.definition}
             </Text>
            </View>
          </View>         
             )
             :null
          }
          </View>
         </View>

      )
   }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  inputBoxContainer: {
    flex: 0.3,
    alignItems: 'center',
    justifyContent: 'center'

  },
  inputBox: {
    width: '80&',
    height: 40,
    alignSelf: 'center',
    textAlign: 'center',
    borderWidth: 4,
  },
  searchButton: {
    width: '29%',
    height: 40,
    alignItems: 'center',
    justifyContent: 'center',
    margin: 10,
    boderWidth: 2,
    borderRadius: 10,
  },
  searchText: {
    fontSize: 20,
    fontWeight: 'bold'
  },
  outputContainer: {
    flex: 0.7,
    alignItems: 'center'
  },
  detailsContainer: {
   flexDirection: 'row',
   alignItems: 'center'
  },
  detailsTitle: {
    color: 'pink',
    fontSize: 20,
    fontWeight:'bold'
  }
});

  
