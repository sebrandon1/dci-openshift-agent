# OpenShift using virtual machines emulating baremetal

Please refer to Google Doc (dci-openshift-agent-linchpin)

## steps ##
Initial Setup

- Install CentOS 7
- Install DCI repo
  % sudo yum install https://packages.distributed-ci.io/dci-release.el7.noarch.rpm
- Install Epel repo
  % sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
- Upgrade to latest versions
  % sudo yum upgrade
- Install DCI openshift agwent
  % sudo yum install dci-openshift-agent

- For either Real or virtual hardware you need to configure
  your DCI authentication
  % sudo vi /etc/dci-openshift-agent/dcirc.sh
  DCI_CLIENT_ID='' # Populate this with your setting
  DCI_API_SECRET='' # Populate this with your setting
  DCI_CS_URL='https://api.distributed-ci.io/'
  export DCI_CLIENT_ID
  export DCI_API_SECRET
  export DCI_CS_URL

- Become user dci-openshift-agent
  # su - dci-openshift-agent
- Run libvirt_create playbook to configure libvirt nodes
  % cd ~/samples/ocp_on_libvirt
  % ansible-playbook -v libvirt_up.yml
- Copy the newly created hosts to /etc/dci-openshift-agent
  % sudo cp hosts /etc/dci-openshift-agent/