# README.md

"""
This is a collection of DevOps scripts for automating various tasks.
"""

import os
import sys

def run_script(script_name):
    """
    Run a script with the given name.

    Args:
        script_name (str): The name of the script to run.

    Returns:
        int: The exit status of the script.
    """
    script_path = os.path.join(os.path.dirname(__file__), script_name)
    if os.path.exists(script_path):
        try:
            with open(script_path, 'r') as f:
                code = compile(f.read(), script_path, 'exec')
                exec(code)
                return 0
        except Exception as e:
            print(f"Error running script {script_name}: {e}")
            return 1
    else:
        print(f"Script {script_name} not found")
        return 1

def main():
    """
    Run the scripts in the scripts directory.
    """
    scripts_dir = os.path.join(os.path.dirname(__file__), 'scripts')
    for filename in os.listdir(scripts_dir):
        if filename.endswith('.py'):
            script_name = os.path.join(scripts_dir, filename)
            sys.exit(run_script(script_name))

if __name__ == '__main__':
    main()