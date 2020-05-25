# Problem statement
> For the form with id "satifaction", we want to check the following rules:
    - Rule 1: "donate" may be checked only if "satisfied" is selected.
    - Rule 2: If "not satisfied" is selected, "reason" must a non-empty string.
If one or both of these rules fail, an appropriate error message should be displayed in the provided div (class "error-message"):

Implement the validateInput function, which returns true when data is valid or false if data is not valid while updating the error message.

```js
function validateInput() {
    // Write your code here.            
}
document.body.innerHTML = `
<!-- Display error message in following div -->
<div class="error-message"></div>

<form id="satisfaction" onsubmit="return validateInput()">
  <input type="radio" name="satisfied" required checked="checked" /> Satisfied
  <input type="checkbox" name="donate" /> Donate<br />
  <input type="radio" name="satisfied" required /> Not satisfied
  <input type="text" name="reason" /> Reason<br />
  <input type="submit" value="Submit" />
</form>`;

validateInput();
            
console.log(document.getElementsByClassName("error-message")[0].innerHTML);
```
## Solution

```html
<script type='text/javascript'>

  function validateInput() {
      // Write your code here.
      const radioButtons = document.getElementsByName('satisfied');
      const donateDom = document.getElementsByName('donate')[0];
      const reasonDom = document.getElementsByName('reason')[0];

      const statisfied = radioButtons[0].checked;
      const donate = donateDom.checked;
      const reason = reasonDom.value;

      let firstRuleInvalid = false, secondRuleInvalid = false;
      if (donate && !statisfied) {
          firstRuleInvalid = true;
      }
      if ((reason && statisfied) || (!statisfied && !reason)) {
          secondRuleInvalid = true;
      }

      const errorDiv = document.getElementsByClassName('error-message')[0];
      if (firstRuleInvalid && secondRuleInvalid) {
          errorDiv.innerHTML = 'BOTH RULES FAILED';
          return false;
      } else if (firstRuleInvalid) {
          errorDiv.innerHTML = 'RULE 1 FAILED';
          return false;
      }
      else if (secondRuleInvalid) {
          errorDiv.innerHTML = 'RULE 2 FAILED';
          return false;
      }
      return true;
  }

  document.body.innerHTML = `
              <!-- Display error message in following div -->
              <div class="error-message"></div>
  
              <form id="satisfaction" onsubmit="return validateInput()">
              <input type="radio" name="satisfied" required checked="checked" /> Satisfied
              <input type="checkbox" name="donate" /> Donate<br />
              <input type="radio" name="satisfied" required /> Not satisfied
              <input type="text" name="reason" /> Reason<br />
              <input type="submit" value="Submit" />
              </form>`;

  validateInput();
  console.log(document.getElementsByClassName("error-message")[0].innerHTML);
</script>
```