# ServiceNow - Implement Client Script & UI Policy

This project implements Client Scripts for Incident table validations as part of SkillWallet Project.

**Table:** Incident [incident]

### 1. Client Script: Auto set urgency for high impact
- **Name:** Auto set urgency for high impact
- **Table:** Incident
- **Type:** onChange
- **Field:** Impact
- **Active:** true
**Script:**
function onChange(control, oldValue, newValue, isLoading) {
    if (isLoading || newValue == '') { return; }
    if (newValue == '1') {
        g_form.setValue('urgency', '1');
        g_form.addInfoMessage('Urgency set to High for High impact incident.');
    }
}

### 2. Client Script: Prevent save if Assigned To missing
- **Name:** Prevent save if Assigned To missing
- **Table:** Incident
- **Type:** onSubmit
- **Active:** true
**Script:**
function onSubmit() {
    if (g_form.getValue('impact') == '1' && g_form.getValue('assigned_to') == '') {
        g_form.showErrorBox('assigned_to','Assigned To is mandatory for High impact incidents.');
        return false;
    }
    return true;
}

### 3. Client Script: Prevent state change via list edit
- **Name:** Prevent state change via list edit
- **Table:** Incident
- **Type:** onCellEdit
- **Field:** State
- **Active:** true
**Script:**
function onCellEdit(sysIDs, table, oldValues, newValue, callback) {
    alert('State cannot be updated using list editing. Please open the Incident.');
    callback(false);
}

### Proof
Demo Link: https://drive.google.com/file/d/1Ts5eurPswjviJ_56xJY-qXCO0pSMViab/view?usp=sharing
