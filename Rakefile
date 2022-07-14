require "rake"
require "rake/clean"
require 'etc'

task default: :test

CLEAN.include FileList["_site"]

task :jekyll do
  require "jekyll"
  Jekyll::Commands::Build.process({ future: true })
end

desc "Run html proofer to validate the HTML output."
task test: :jekyll do
  require "html-proofer"

  HTMLProofer.check_directory(
    "./_site",
    allow_hash_href: false,
    allow_missing_href: false,
    cache: {
      timeframe: {
        external: '1h'
      }
    },
    check_external_hash: true,
    check_favicon: true,
    check_opengraph: true,
    check_html: true,
    check_img_http: true,
    enforce_https: true,
    ignore_empty_alt: false,
    ignore_status_codes: [0, 302, 303, 429, 521],
    ignore_urls: [
    ],
    parallel: { in_processes: Etc.nprocessors },
    validation: {
      report_eof_tags: true,
      report_invalid_tags: true,
      report_mismatched_tags: true,
      report_missing_doctype: true,
      report_missing_names: true,
      report_script_embeds: true,
    }
  ).run
end
