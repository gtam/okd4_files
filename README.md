# okd4_files

See https://medium.com/swlh/guide-okd-4-5-single-node-cluster-832693cb752b for full guide.  Below pushit and wrapit scripts are just commands from guide.

Pull the branch
- git pull -b snc https://github.com/gtam/okd4_files.git

Rename and edit files as needed

Run the pushit script to install components
- okd4_files/pushit

Startup bootstrap, control-plane, and worker nodes

Run the wrapit script to finish the rest of steps
- okd4_files/wrapit
