#!/bin/bash

##
# The MIT License (MIT)
# 
# Copyright (c) 2024 Jacky Xie
# 
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
# 
# The above copyright notice and this permission notice shall be included in
# all copies or substantial portions of the Software.
# 
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
# THE SOFTWARE.
##

install_fws() {
  if ! [ -d /tmp/fws_install ]; then
    mkdir /tmp/fws_install
  fi

  wget https://raw.githubusercontent.com/fafnirZ/fuzz_workspace/refs/heads/main/fws \
     -O /tmp/fws_install/fws \
     -q
  if [ $? -ne 0 ]; then
    echo "$ERROR failed to install fws $CLEAR"
    exit 1
  fi 

  # check bin checksum
  original_checksum=$(curl https://raw.githubusercontent.com/fafnirZ/fuzz_workspace/refs/heads/main/checksum)
  new_checksum=$(cat /tmp/fws_install/fws | md5sum | cut -d' ' -f1)
  diff <(echo $original_checksum) <(echo $new_checksum)
  if [ $? -ne 0 ];then
    echo "$ERROR ERROR CHECKSUMS DONT MATCH $CLEAR" 
    exit 1
  fi

  # move to /usr/local/bin
  sudo cp fws /usr/local/bin

  # cleanup
  cd /tmp/fws_install
  rm -r /tmp/fws_install
  echo "cleaned up /tmp/fws_install"

}