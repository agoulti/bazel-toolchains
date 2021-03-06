# Copyright 2017 The Bazel Authors. All rights reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

load("//rules/experimental/rbe:exec_properties.bzl", "create_exec_properties_dict")

# Test the docker_privileged property
constraint_setting(name = "constraint_privileged")

constraint_value(
    name = "constraint_privileged_on",
    constraint_setting = ":constraint_privileged",
)

platform(
    name = "platform_privileged_on",
    constraint_values = [":constraint_privileged_on"],
    exec_properties = create_exec_properties_dict(docker_privileged = True),
    parents = ["@rbe_default_exec_properties//config:platform"],
)

# privileged_off_test should run with @rbe_default_exec_properties//config:platform
sh_test(
    name = "privileged_off_test",
    srcs = ["privileged_off.sh"],
)

# privileged_on_test should run with :platform_privileged_on
sh_test(
    name = "privileged_on_test",
    srcs = ["privileged_on.sh"],
    exec_compatible_with = [
        ":constraint_privileged_on",
    ],
)

# Test the docker_network_enabled property
constraint_setting(name = "constraint_network")

constraint_value(
    name = "constraint_network_enabled",
    constraint_setting = ":constraint_network",
)

platform(
    name = "platform_network_enabled",
    constraint_values = [":constraint_network_enabled"],
    exec_properties = create_exec_properties_dict(docker_network_enabled = True),
    parents = ["@rbe_default_exec_properties//config:platform"],
)

# network_disabled_test should run with @rbe_default_exec_properties//config:platform
sh_test(
    name = "network_disabled_test",
    srcs = ["network_disabled.sh"],
)

# network_enabled_test should run with :platform_network_enabled
sh_test(
    name = "network_enabled_test",
    srcs = ["network_enabled.sh"],
    exec_compatible_with = [
        ":constraint_network_enabled",
    ],
)
