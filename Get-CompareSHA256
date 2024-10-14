# Add the .NET assembly for forms to display a message box and input box
$filePath = $args[0]

Add-Type -AssemblyName System.Windows.Forms

# Function to compute SHA-256 hash of a file
function Get-FileHashSHA256 {
    param (
        [string] $file
    )
    
    if (Test-Path $file) {
        $sha256 = Get-FileHash -Algorithm SHA256 -Path $file
        return $sha256.Hash
    } else {
        return "File not found."
    }
}

# Function to create and show an input form to get a comparison hash
function ShowComparisonForm {
    param (
        [string]$calculatedHash
    )
    
    # Create the form
    $form = New-Object Windows.Forms.Form
    $form.Text = "SHA-256 Hash Comparison"
    $form.Width = 500
    $form.Height = 250

    # Label for the calculated hash
    $labelHash = New-Object Windows.Forms.Label
    $labelHash.Text = "Calculated SHA-256 Hash:"
    $labelHash.Top = 20
    $labelHash.Left = 10
    $labelHash.AutoSize = $true
    $form.Controls.Add($labelHash)

    # Text box for displaying the calculated hash (read-only)
    $textBoxHash = New-Object Windows.Forms.TextBox
    $textBoxHash.Text = $calculatedHash
    $textBoxHash.Width = 450
    $textBoxHash.Top = 40
    $textBoxHash.Left = 10
    $textBoxHash.ReadOnly = $true
    $form.Controls.Add($textBoxHash)

    # Label for comparison input
    $labelInput = New-Object Windows.Forms.Label
    $labelInput.Text = "Enter Hash for Comparison:"
    $labelInput.Top = 80
    $labelInput.Left = 10
    $labelInput.AutoSize = $true
    $form.Controls.Add($labelInput)

    # Text box for the user to input the comparison hash
    $textBoxInput = New-Object Windows.Forms.TextBox
    $textBoxInput.Width = 450
    $textBoxInput.Top = 100
    $textBoxInput.Left = 10
    $form.Controls.Add($textBoxInput)

    # Label for showing the result of the comparison
    $labelResult = New-Object Windows.Forms.Label
    $labelResult.Text = ""
    $labelResult.Top = 160
    $labelResult.Left = 10
    $labelResult.AutoSize = $true
    $form.Controls.Add($labelResult)

    # OK Button to compare the hashes
    $okButton = New-Object Windows.Forms.Button
    $okButton.Text = "Compare"
    $okButton.Top = 130
    $okButton.Left = 150
    $okButton.Add_Click({
        if ($calculatedHash -eq $textBoxInput.Text) {
            $labelResult.Text = "Result: Hashes Match!"
        } else {
            $labelResult.Text = "Result: Hashes Do Not Match!"
        }
    })
    $form.Controls.Add($okButton)

    # Show the form
    $form.ShowDialog()
}


# Calculate the file's SHA-256 hash
$calculatedHash = Get-FileHashSHA256 $filePath

# Show the comparison form with the calculated hash
ShowComparisonForm -calculatedHash $calculatedHash
