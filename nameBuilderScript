function nameBuilder() {
  let ss = SpreadsheetApp.getActiveSpreadsheet();
  
  // Retrieve values and filter out empty entries
  let domains = [...new Set(ss.getRange('A3:A999').getValues().flat().filter(thing => thing !== ''))];
  let locations = [...new Set(ss.getRange('B3:B999').getValues().flat().filter(thing => thing !== ''))];
  let frequency = [...new Set(ss.getRange('C3:C999').getValues().flat().filter(thing => thing !== ''))];
  let consentScenario = [...new Set(ss.getRange('D3:D999').getValues().flat().filter(thing => thing !== ''))];
  let additionalSettingOne = [...new Set(ss.getRange('E3:E999').getValues().flat().filter(thing => thing !== ''))];
  let additionalSettingTwo = [...new Set(ss.getRange('F3:F999').getValues().flat().filter(thing => thing !== ''))];
  
  let auditNames = [];
  let space = " - ";

  // Function to build audit name
  function auditNameBuilder(params) {
    return params.join(space);
  }

  // Create a helper function to build combinations
  function buildCombinations() {
    let paramSets = [domains, locations, frequency, consentScenario, additionalSettingOne, additionalSettingTwo];
    
    // Filter out empty parameter sets
    paramSets = paramSets.filter(set => set.length > 0);
    
    // Handle case when no parameters are provided
    if (paramSets.length === 0) return;

    // Recursive function to generate combinations
    function combine(currentParams, depth) {

      if (depth === paramSets.length) {
        auditNames.push(auditNameBuilder(currentParams));
        return;
      }
      
      for (let item of paramSets[depth]) {
        combine([...currentParams, item], depth + 1);
      }
    }
    
    // Start recursion with an empty current parameter array
    combine([], 0);
  }

  // Generate combinations
  buildCombinations();

  // Clear output column
  let outputRange = ss.getRange('H3:H' + (auditNames.length + 2));
  ss.getRange('H3:H999').clearContent();

  // Batch write the array to the sheet
  let outputData = auditNames.map(name => [name]); // Convert 1D array to 2D for setValues
  outputRange.setValues(outputData);

  console.log(auditNames.length)
}
