# Web Application Penetration Testing Toolkit

A comprehensive guide for setting up a web application security testing environment and conducting reconnaissance .

## 🚀 Quick Start

1. Set up your environment with the system prerequisites
2. Install the required tools
3. Configure your testing environment
4. Run the reconnaissance workflow

## 📋 Table of Contents

- [System & Language Installation](#system--language-installation)
- [Tool Installation](#tool-installation)
- [Utility Configuration](#utility-configuration)
- [Reconnaissance Workflow](#reconnaissance-workflow)
- [Usage Examples](#usage-examples)
- [Contributing](#contributing)
- [Disclaimer](#disclaimer)

## System & Language Installation

Python 3 Installation
Run the following commands to install Python 3, pip, and virtual environment support:
```bash
sudo apt-get update -y
sudo apt-get dist-upgrade -y
sudo apt install -y python3 python3-pip python3.12-venv
Verify the installation with:
python3 --version
pip3 --version
```
Golang Installation
Run the following commands to install the Go programming language:
```
sudo apt-get update -y
sudo apt-get dist-upgrade -y
wget https://go.dev/dl/go1.23.3.linux-amd64.tar.gz
rm -rf /usr/local/go
sudo tar -C /usr/local -xzf go1.23.3.linux-amd64.tar.gz
Add Go to your system's PATH by editing your shell configuration file (.bashrc or .zshrc):
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
echo 'export PATH=$PATH:~/go/bin' >> ~/.bashrc
Apply the changes and verify:
source ~/.bashrc
go version
Clean up the downloaded archive:
rm -rf go1.23.3.linux-amd64.tar.gz
```
C-Make Installation
Install CMake, a cross-platform build system, with:
```
sudo apt-get update -y
sudo apt-get dist-upgrade -y
sudo apt install cmake -y
```
Rust Installation
Install the Rust programming language using rustup:
```
sudo apt-get update -y
sudo apt-get dist-upgrade -y
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
Source the environment and verify:
source $HOME/.cargo/env
rustc --version
```
Tool Installation Guide
Reconnaissance & Discovery Tools
```
urldedupe
A tool to deduplicate URLs. Clone, build, and install it:
git clone https://github.com/ameraman/urldedupe.git
cd urldedupe
cmake CMakeLists.txt
make
sudo cp urldedupe /usr/local/bin/
cd ../
Test the installation: urldedupe -h
```

Arjun (HTTP Parameter Discovery)
Discovers hidden HTTP parameters. Install via a Python virtual environment:
```
git clone https://github.com/s0md3w/Arjun.git
python3 -m venv arjun-env
source arjun-env/bin/activate
cd Arjun
pip3 install .
sudo cp ~/arjun-env/bin/arjun /usr/local/bin/
deactivate
cd ../
Test the installation: arjun -h
```

Waymore (Content Discovery)
Finds URLs from various sources. Install via a Python virtual environment:
```
git clone https://github.com/xnl-h4ck3r/waymore.git
python3 -m venv waymore-env
source waymore-env/bin/activate
cd waymore
pip3 install .
pip3 install -r requirements.txt
sudo cp ~/waymore-env/bin/waymore /usr/local/bin/
deactivate
cd ../
Test the installation: waymore -h
```
Sublist3r (Subdomain Enumeration)
Enumerates subdomains. Install via a Python virtual environment:
```
git clone https://github.com/aboul3la/Sublist3r.git
python3 -m venv sublist3r-env
source sublist3r-env/bin/activate
cd Sublist3r
pip3 install .
pip3 install -r requirements.txt
sudo cp ~/sublist3r-env/bin/sublist3r /usr/local/bin/
deactivate
cd ../
Test the installation: sublist3r -h
```

Dirsearch (Web Path Scanner)
A mature web path scanner. Install via a Python virtual environment:
```
git clone https://github.com/maurosoria/dirsearch.git --depth 1
python3 -m venv dirsearch-env
source dirsearch-env/bin/activate
cd dirsearch
pip3 install .
pip3 install -r requirements.txt
sudo cp ~/dirsearch-env/bin/dirsearch /usr/local/bin/
deactivate
cd ../
Test the installation: dirsearch -h
```

subExtreme (Subdomain Enumeration)
A fast subdomain enumerator written in Rust. Install its dependencies first:
```
sudo apt-get update -y
sudo apt-get dist-upgrade -y
sudo apt install pkg-config -y
sudo apt install libssl-dev -y
Clone, build, and install:
git clone https://github.com/ahmedkhlief/subextreme.git
cd subextreme
cargo build --release
sudo cp target/release/subextreme /usr/local/bin/
sudo chmod +x /usr/local/bin/subextreme
cd ../
Test the installation: subextreme -h
```

Httpx (HTTP Toolkit)
A fast and multi-purpose HTTP toolkit. Remove old versions and install the latest with Go:
```
sudo rm -f /usr/bin/httpx
sudo apt remove httpx -y
go install -v github.com/projectdiscovery/httpx/cmd/httpx@latest
Test the installation: httpx -h
```

Crawley (Advanced Web Crawler)
A powerful web crawler. Download the pre-built binary and install it:
```
mkdir crawley
cd crawley
wget https://github.com/s8rg/crawley/releases/download/v1.7.18/crawley_v1.7.19_linux_x86_64.tar.gz
tar -xvzf crawley_v1.7.19_linux_x86_64.tar.gz
sudo cp crawley /usr/local/bin/
cd ../
Test the installation: crawley -h
```

Fuzzing & Testing Tools
PassURLs (Proxy Tool)
A tool to pass URLs through a proxy. Install via a Python virtual environment:
```
git clone https://github.com/ahmedkhlief/passurls.git
python3 -m venv passurls-env
source passurls-env/bin/activate
cd passurls
pip3 install .
pip3 install -r requirements.txt
sudo cp ~/passurls-env/bin/passurls /usr/local/bin/
deactivate
cd ../
Test the installation: passurls -h
```
Dalfox (XSS Scanner)
A powerful XSS scanning tool. Install it with Go:

go install ```github.com/hahwul/dalfox/v2@latest```
Test the installation: dalfox -h

Wordlists
Seelists
A collection of curated wordlists useful for brute-forcing and discovery.
```git clone https://github.com/danielmiessler/Seelists.git```

Utility Configuration
Import Burp Suite Certificate
To intercept HTTPS traffic without errors, import Burp Suite's CA certificate into your system's trust store.
First, export the certificate from Burp Suite in DER format (e.g., to ~/burp.der).
Convert and copy the certificate:
```
openssl x509 -inform DER -in ~/burp.der -out ~/burp-ca.crt
sudo cp ~/burp-ca.crt /usr/local/share/ca-certificates/
Update the CA certificate store:
sudo update-ca-certificates
```
Reconnaissance Workflow
1. Initial Setup
Create an organized directory structure for your target.
```
mkdir bugbounty
cd bugbounty
mkdir target
cd target
```
3. Subdomain Enumeration
Use multiple tools to discover subdomains for a comprehensive view.
```
sublist3r -d example.com -b -t 50 -v -o sublist3r.txt
subextreme -w ~/SecLists/Discovery/DNS/subdomains.txt -d example.com -c 100 -o subextreme.txt
Combine and deduplicate the results:
cat sublist3r.txt subextreme.txt | urldedupe -s > subdomains.txt
```
5. URL Discovery (Waymore)
Passively discover URLs from the enumerated subdomains.
```
waymore -i subdomains.txt -o waymore_urls.txt
Extract unique URLs:
cat waymore_urls.txt | urldedupe > unique_urls.txt
```

5. Proxy URLs through Burp Suite
Send the discovered URLs through Burp Suite for passive analysis and traffic inspection.
```
passurls -p 127.0.0.1:8080 -i unique_urls.txt
```
7. Deep Crawling (Through Proxy)
Perform an active, deep crawl of the target while routing all traffic through Burp Suite for detailed inspection. Warning: This is resource-intensive.
Set environment variables to use the proxy:
```
export http_proxy="http://127.0.0.1:8080"
export https_proxy="http://127.0.0.1:8080"
export ALL_PROXY="http://127.0.0.1:8080"
```
Run Crawley with specific options:
```
crawley --headless --delay 30ms --depth -1 --subdomains --all --timeout 30s --user-agent "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36" https://example.com/ | tee crawley.txt
```

7. Process Results & Parameter Extraction
After manual testing in Burp, save all interesting URLs to a file (e.g., burp-results.txt).
Extract parameters from these URLs:
```
grep -E "\?.*=" burp-results.txt > burp-params.txt
Deduplicate the parameters:
cat burp-params.txt | urldedupe -w > parameters.txt
```
9. Discover Hidden Parameters
Use Arjun to find parameters not discovered through crawling.
```
arjun -i urls.txt -t 10 -T 80 -d 40 -pb http://127.0.0.1:8080 -m POST -o hidden-params.txt
```
11. XSS Vulnerability Scanning
Scan all discovered parameters for XSS vulnerabilities using Dalfox.
```
dalfox file parameters.txt --user-agent "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36" --timeout 30 --proxy http://127.0.0.1:8080 -o dalfox.txt --deep-domxss
```

