# XxkarizmaxX-FIM


Write-Host ""
write-Host "what would you like to do?"
write-Host "A) collect new Baseline?"
write-Host "B) begin monitoring files with saved Baseline?"

$response = read-host -prompt "please enter 'A' or 'B'"
Write-Host ""

Function Calculate-File-Hash($filepath) {
    $filehash = Get-FileHash -Path $filepath -Algorithm SHA512
    return $filehash
}


if ($response -eq "A".ToUpper()) {
    # Calculate hash from the target files and store in baseline.txt
    
    # Collect all files in the target folder
    $files = Get-ChildItem -Path .\Files

    # For file, Calculate the hash, and write to basline.txt
    foreach ($f in $files) {
        $hash = Calculate-File-Hash $f.FULLName
        "$($hash.Path)|$($hash.Hash)"
    }
}

elseif ($response -eq "B".ToUPPER()) {
    # Begin monitoring files with saved Baseline
    Write-host "read existing baseline.txt, start monitoring files." -ForegroundColor Yellow
}

